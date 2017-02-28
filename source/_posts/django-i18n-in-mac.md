---
title: django i18n in mac
tags:
  - django
date: 2016-09-27 23:32:00
---

First, install gettext

<pre class="prettyprint">brew install gettext
brew link gettext --force
</pre>
Add "locale" folder in your project root or app root.

In settings.py
Add to MIDDLEWEAR_CLASSES, locale, it enables language selection based on request:
'django.middleware.locale.LocaleMiddleware',
Add LOCALE_PATHS, this is where your translation files will be stored:
<pre class="prettyprint">LOCALE_PATHS = (
    os.path.join(PROJECT_PATH, 'locale/'),
)
</pre>

In your template,
```
{% load i18n %}
{% trans "XXX" %}
```

In command line,
django-admin makemessages -l zh-hant
django-admin.py compilemessages -l zh-hant

In urls.py
<pre class="prettyprint">from django.conf.urls import include, url
from django.conf.urls.i18n import i18n_patterns
from django.contrib import admin

urlpatterns = [
    url(r'^admin/', include(admin.site.urls)),
]

urlpatterns += i18n_patterns(
    url(r'^$', 'home.views.index'),
)
</pre>

Reference:
[http://missions5.blogspot.tw/2015/03/django-1.html](http://missions5.blogspot.tw/2015/03/django-1.html)
[http://blog.blackwhite.tw/2013/04/django-i18n.html](http://blog.blackwhite.tw/2013/04/django-i18n.html)
[http://stackoverflow.com/questions/10280881/django-site-with-2-languages](http://stackoverflow.com/questions/10280881/django-site-with-2-languages)
