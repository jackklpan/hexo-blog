---
title: django Elastic Beanstalk
tags:
  - django
date: 2015-10-21 15:03:00
---

Opswork
https://github.com/poise/poise-python

Elastic Beanstalk
http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/create-deploy-python-django.html
http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/installing-ebcli.html

http://blog.amowu.com/2015/04/devops-continuous-integration-delivery-docker-circleci-aws-beanstalk.html?m=1

Good tutorial:
[https://realpython.com/blog/python/deploying-a-django-app-to-aws-elastic-beanstalk/](https://realpython.com/blog/python/deploying-a-django-app-to-aws-elastic-beanstalk/)
Below are simple notes.

### eb init

Default region

Choosing the region closest to your end users will generally provide the best performance. Check out [this map](http://www.turnkeylinux.org/blog/aws-datacenters) if you’re unsure which to choose.

Credentials

Next, it’s going to ask for your AWS credentials.

Here, you will most likely want to set up an IAM User. See this guide for how to set one up. If you do set up a new user you will need to ensure the user has the appropriate permissions. The simplest way to do this is to just add “Administrator Access” to the User. (This is probably not a great choice for security reasons, though.) For the specific policies/roles that a user needs in order to create/manage an Elastic Beanstalk application, see the link here.

Application name

This will default to the directory name. Just go with that.

Python version

Next, the CLI should automagically detect that you are using Python and just ask for confirmation. Say yes. Then you need to select a platform version. Select Python 2.7.

SSH

Say yes to setting up SSH for your instances.

RSA Keypair

Next, you need to generate an RSA keypair, which will be added to your ~/.ssh folder. This keypair will also be uploaded to the EC2 public key for the region you specified in step one. This will allow you to SSH into your EC2 instance later in this tutorial.

### eb create

Environment Name

You should use a similar naming convention to what Amazon suggest – e.g., application_name-env_name – especially when/if you start hosing multiple applications with AWS. I used – iod-test.

DNS CNAME prefix

When you deploy an app to Elastic Beanstalk you will automatically get a domain name like xxx.elasticbeanstalk.com. DNS CNAME prefix is what you want to be used in place of xxx. Just go with the default.

### Installing packages

The first thing we need to do is install some packages so that our pip install command will complete successfully. To do this, let’s first create a file called .ebextensions/01_packages.config:

packages:
&nbsp; yum:
&nbsp; &nbsp; git: []
&nbsp; &nbsp; postgresql93-devel: []
EC2 instances run Amazon Linux, which is a Redhat flavor, so we can use yum to install the packages that we need. For now, we are just going to install two packages – git and the Postgres client.

To use the .config file option, let’s create a new file called /.ebextensions/02_python.config:

option_settings:
&nbsp; "aws:elasticbeanstalk:application:environment":
&nbsp; &nbsp; DJANGO_SETTINGS_MODULE: "iotd.settings"
&nbsp; &nbsp; "PYTHONPATH": "/opt/python/current/app/iotd:$PYTHONPATH"
&nbsp; "aws:elasticbeanstalk:container:python":
&nbsp; &nbsp; WSGIPath: iotd/iotd/wsgi.py
&nbsp; &nbsp; NumProcesses: 3
&nbsp; &nbsp; NumThreads: 20
&nbsp; "aws:elasticbeanstalk:container:python:staticfiles":
&nbsp; &nbsp; "/static/": "www/static/"
What’s happening?

DJANGO_SETTINGS_MODULE: "iotd.settings" – adds the path to the settings module.
"PYTHONPATH": "/opt/python/current/app/iotd:$PYTHONPATH" – updates our PYTHONPATH so Python can find the modules in our application. (Note that the use of the full path is necessary.)
WSGIPath: iotd/iotd/wsgi.py sets our WSGI Path.
NumProcesses: 3 and NumThreads: 20 – updates the number of processes and threads used to run our WSGI application.
"/static/": "www/static/" sets our static files path.

container_commands:
&nbsp; 01_migrate:
&nbsp; &nbsp; command: "source /opt/python/run/venv/bin/activate &amp;&amp; python iotd/manage.py migrate --noinput"
&nbsp; &nbsp; leader_only: true
&nbsp; 02_createsu:
&nbsp; &nbsp; command: "source /opt/python/run/venv/bin/activate &amp;&amp; python iotd/manage.py createsu"
&nbsp; &nbsp; leader_only: true
&nbsp; 03_collectstatic:
&nbsp; &nbsp; command: "source /opt/python/run/venv/bin/activate &amp;&amp; python iotd/manage.py collectstatic --noinput"

option_settings:
&nbsp; "aws:elasticbeanstalk:application:environment":
&nbsp; &nbsp; DJANGO_SETTINGS_MODULE: "iotd.settings"
&nbsp; &nbsp; "PYTHONPATH": "/opt/python/current/app/iotd:$PYTHONPATH"
&nbsp; &nbsp; "ALLOWED_HOSTS": ".elasticbeanstalk.com"
&nbsp; "aws:elasticbeanstalk:container:python":
&nbsp; &nbsp; WSGIPath: iotd/iotd/wsgi.py
&nbsp; &nbsp; NumProcesses: 3
&nbsp; &nbsp; NumThreads: 20
&nbsp; "aws:elasticbeanstalk:container:python:staticfiles":
&nbsp; &nbsp; "/static/": "www/static/"

We now need to ensure that the STATIC_ROOT is set correctly in the settings.py file:

STATIC_ROOT = os.path.join(BASE_DIR, "..", "www", "static")
STATIC_URL = '/static/'