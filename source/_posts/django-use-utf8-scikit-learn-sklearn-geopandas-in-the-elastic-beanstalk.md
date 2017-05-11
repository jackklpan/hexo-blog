---
title: django use utf8 + scikit-learn ( sklearn ) + geopandas in the elastic beanstalk
tags:
  - django
date: 2016-12-29 23:07:00
---

### General EB Settings
Use t2.small, otherwise the memory will not enough.

```
commands:
  000_dd:
    command: test -f /swapfile || dd if=/dev/zero of=/swapfile bs=1024 count=1500000
  001_mkswap:
    command: test -f /swapfile || mkswap /swapfile
  002_chmod:
    command: test -f /swapfile || chmod 0600 /swapfile
  003_swapon:
    command: test -f /swapfile || swapon /swapfile
```

```
packages:
  yum:
    git: []
    postgresql93-devel: []
    atlas-devel: []
    atlas-sse3-devel: []
    blas-devel: []
    gcc: []
    gcc-c++: []
    lapack-devel: []
    python34-devel: []
    libpng-devel: []
    freetype-devel: []
    geos: []

sources:
  /home/ec2-user: http://download.osgeo.org/gdal/1.11.2/gdal1112.zip

commands:
  04_install_gdal:
    cwd: /home/ec2-user/gdal-1.11.2
    command: test -e gdal-check.txt || ./configure --with-python=yes && make && sudo make install && echo 'ok' > gdal-check.txt
```

```
container_commands:
  01_collectstatic:
    command: "source /opt/python/run/venv/bin/activate && source /opt/python/current/env && python manage.py collectstatic --noinput"
  02_migrate:
    command: "source /opt/python/run/venv/bin/activate && source /opt/python/current/env && python manage.py migrate --noinput"
    leader_only: true
  03_wsgi_custom:
    command: 'cp .ebextensions/wsgi.conf /opt/python/ondeck/wsgi.conf'

option_settings:
  "aws:elasticbeanstalk:application:environment":
    DJANGO_SETTINGS_MODULE: "xxx.settings_production"
    "PYTHONPATH": "/opt/python/current/app/xxx:$PYTHONPATH"
  "aws:elasticbeanstalk:container:python":
    WSGIPath: "xxx/wsgi.py"
  "aws:elasticbeanstalk:container:python:staticfiles":
    "/static/": "www/static/"
```

wsgi
```

LoadModule wsgi_module modules/mod_wsgi.so
WSGIPythonHome /opt/python/run/baselinenv
WSGISocketPrefix run/wsgi
WSGIRestrictEmbedded On

<VirtualHost *:80>

Alias /static/ /opt/python/current/app/www/static/
<Directory /opt/python/current/app/www/static/>
Order allow,deny
Allow from all
</Directory>


WSGIScriptAlias / /opt/python/current/app/xxx/wsgi.py


<Directory /opt/python/current/app/>
  Require all granted
</Directory>

WSGIDaemonProcess wsgi processes=1 threads=15 display-name=%{GROUP} \
  python-path=/opt/python/current/app:/opt/python/run/venv/lib64/python3.4/site-packages:/opt/python/run/venv/lib/python3.4/site-packages user=wsgi group=wsgi \
  home=/opt/python/current/app lang=en_US.UTF-8 locale=en_US.UTF-8
WSGIProcessGroup wsgi
</VirtualHost>

LogFormat "%h (%{X-Forwarded-For}i) %l %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-Agent}i\"" combined

WSGIApplicationGroup %{GLOBAL}
```

Make sure place packages in the requirements.txt in the correct order (dependency). Place Scipy before scikit-learn.

### Geopandas
requirements.txt Shapely==1.5.17.post1 => Shapely==1.5.17

```eb deploy --timout 3600```. Otherwise it will timeout to build gdal.

In AWS EB Web interface => configuration --> software configuration and edited the Environment Properties by adding the property LD_LIBRARY_PATH set as /usr/local/lib/:$LD_LIBRARY_PATH.

### UTF-8
And if encounter the utf-8 encoding problems in EB.
1. You can add ```.encode('utf-8')``` if there are non-ascii char in the string.
2. Change wsgi.conf which in the /etc/httpd/conf.d/wsgi.conf

WSGIDaemonProcess wsgi processes=1 threads=15 display-name=%{GROUP} \
  python-path=/opt/python/current/app:/opt/python/run/venv/lib64/python3.4/site-packages:/opt/python/run/venv/lib/python3.4/site-packages user=wsgi group=wsgi \
  home=/opt/python/current/app **lang=en_US.UTF-8 locale=en_US.UTF-8**
WSGIProcessGroup wsgi

3. ```export LC_ALL=en_US.UTF-8 && export LANG=en_US.UTF-8 && command``` by using subprocess.call([""], shell=True)

### Reference:
[http://stackoverflow.com/questions/25477268/script-timed-out-before-returning-headers-wsgi-py-on-elastic-beanstalk](http://stackoverflow.com/questions/25477268/script-timed-out-before-returning-headers-wsgi-py-on-elastic-beanstalk)
[https://code.google.com/archive/p/modwsgi/wikis/ApplicationIssues.wiki#Python_Simplified_GIL_State_API](https://code.google.com/archive/p/modwsgi/wikis/ApplicationIssues.wiki#Python_Simplified_GIL_State_API)
[http://stackoverflow.com/questions/30634777/unicodeencodeerror-when-running-in-mod-wsgi-even-after-setting-lang-and-lc-all](http://stackoverflow.com/questions/30634777/unicodeencodeerror-when-running-in-mod-wsgi-even-after-setting-lang-and-lc-all)
[http://stackoverflow.com/questions/17326294/configuring-amazon-elastic-beanstalk-with-postgis](http://stackoverflow.com/questions/17326294/configuring-amazon-elastic-beanstalk-with-postgis)
[http://stackoverflow.com/questions/21715423/installing-postgis-on-amazon-elastic-beanstalk-using-config-file](http://stackoverflow.com/questions/21715423/installing-postgis-on-amazon-elastic-beanstalk-using-config-file)
