---
title: Install python 3 in AWS linux by pyenv
tags: [python, aws]
date: 2015-02-23 19:54:00
---

curl -L https://raw.githubusercontent.com/pyenv/pyenv-installer/master/bin/pyenv-installer | bash

vim .bash_profile

add following lines to .bash_profile:
```
export PATH="/home/ec2-user/.pyenv/bin:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"
```

sudo yum install gcc

sudo yum install openssl-devel

sudo yum install bzip2-devel

sudo yum install sqlite-devel

sudo yum install readline-devel

pyenv install 3.4.3
