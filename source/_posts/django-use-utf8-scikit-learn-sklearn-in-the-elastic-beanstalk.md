---
title: django use utf8 + scikit-learn ( sklearn ) in the elastic beanstalk
tags:
  - django
date: 2016-12-29 23:07:00
---

Use t2.small, otherwise the memory will not enough.

commands:
&nbsp; 000_dd:
&nbsp; &nbsp; command: test -f /swapfile || dd if=/dev/zero of=/swapfile bs=1024 count=1500000
&nbsp; 001_mkswap:
&nbsp; &nbsp; command: test -f /swapfile || mkswap /swapfile
&nbsp; 002_chmod:
&nbsp; &nbsp; command: test -f /swapfile || chmod 0600 /swapfile
&nbsp; 003_swapon:
&nbsp; &nbsp; command: test -f /swapfile || swapon /swapfile

packages:
&nbsp; yum:
&nbsp; &nbsp; git: []
&nbsp; &nbsp; postgresql93-devel: []
&nbsp; &nbsp; atlas-devel: []
&nbsp; &nbsp; atlas-sse3-devel: []
&nbsp; &nbsp; blas-devel: []
&nbsp; &nbsp; gcc: []
&nbsp; &nbsp; gcc-c++: []
&nbsp; &nbsp; lapack-devel: []
&nbsp; &nbsp; python34-devel: []
&nbsp; &nbsp; libpng-devel: []
&nbsp; &nbsp; freetype-devel: []
<div>
</div><div>
</div><div>
</div><div><div>container_commands:</div><div>&nbsp; 01_collectstatic:</div><div>&nbsp; &nbsp; command: "source /opt/python/run/venv/bin/activate &amp;&amp; python manage.py collectstatic --noinput"</div><div>&nbsp; 02_wsgi_scipy:</div><div>&nbsp; &nbsp; <span style="color: red;">command: 'echo "WSGIApplicationGroup %{GLOBAL}" &gt;&gt; ../wsgi.conf'</span></div><div>
</div><div>option_settings:</div><div>&nbsp; "aws:elasticbeanstalk:application:environment":</div><div>&nbsp; &nbsp; DJANGO_SETTINGS_MODULE: "your_app_setting"</div><div>&nbsp; &nbsp; "PYTHONPATH": "/opt/python/current/app/your_app:$PYTHONPATH"</div><div>&nbsp; "aws:elasticbeanstalk:container:python":</div><div>&nbsp; &nbsp; WSGIPath: "your_app/wsgi.py"</div><div>&nbsp; "aws:elasticbeanstalk:container:python:staticfiles":</div><div>&nbsp; &nbsp; "/static/": "www/static/"</div></div><div>
</div><div>
Make sure place packages in the requirements.txt in the correct order (dependency).
Ex: place Scipy before scikit-learn.</div><div>

And if encounter the utf-8 encoding problems in EB.</div><div>1\. You can add <span style="color: red;">.encode('utf-8') if there are non-ascii char in the string.</span></div><div>2\. Change wsgi.conf which in the /etc/httpd/conf.d/wsgi.conf
WSGIDaemonProcess wsgi processes=1 threads=15 display-name=%{GROUP} \
&nbsp; python-path=/opt/python/current/app:/opt/python/run/venv/lib64/python3.4/site-packages:/opt/python/run/venv/lib/python3.4/site-packages user=wsgi group=wsgi \
&nbsp; home=/opt/python/current/app <span style="color: red;">lang=en_US.UTF-8 locale=en_US.UTF-8</span>
WSGIProcessGroup wsgi
3.&nbsp;export LC_ALL=en_US.UTF-8 &amp;&amp; export LANG=en_US.UTF-8 &amp;&amp; command by using&nbsp;subprocess.call([""], shell=True) if necessary.

</div><div>Reference:</div><div>[http://stackoverflow.com/questions/25477268/script-timed-out-before-returning-headers-wsgi-py-on-elastic-beanstalk](http://stackoverflow.com/questions/25477268/script-timed-out-before-returning-headers-wsgi-py-on-elastic-beanstalk)</div><div>[https://code.google.com/archive/p/modwsgi/wikis/ApplicationIssues.wiki#Python_Simplified_GIL_State_API](https://code.google.com/archive/p/modwsgi/wikis/ApplicationIssues.wiki#Python_Simplified_GIL_State_API)</div><div>[http://stackoverflow.com/questions/30634777/unicodeencodeerror-when-running-in-mod-wsgi-even-after-setting-lang-and-lc-all](http://stackoverflow.com/questions/30634777/unicodeencodeerror-when-running-in-mod-wsgi-even-after-setting-lang-and-lc-all)</div><div>
</div>