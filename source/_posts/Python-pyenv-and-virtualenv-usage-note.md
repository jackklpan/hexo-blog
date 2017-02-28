---
title: Python pyenv and virtualenv usage note
tags:
  - python
date: 2015-02-09 19:58:00
---

## Installation:
<div>
</div>

### pyenv
<div>
</div>

#### Mac
<div>
</div>brew update
brew install pyenv

To upgrade pyenv in the future, just use upgrade instead of install.

After installation, you'll still need to add eval "$(pyenv init -)" to your profile (add it to ~/.bash_profile). You'll only ever have to do this once.

#### Others
<div>
</div># Get Code
git clone https://github.com/yyuu/pyenv.git ~/.pyenv

# Set the Paths
echo 'export PYENV_ROOT="$HOME/.pyenv"' &gt;&gt; ~/.bash_profile
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' &gt;&gt; ~/.bash_profile
**Zsh note: Modify your ~/.zshenv file instead of ~/.bash_profile.**
**Ubuntu note: Modify your ~/.bashrc file instead of ~/.bash_profile.**

# Initialize pyenv on load of terminal
echo 'eval "$(pyenv init -)"' &gt;&gt; ~/.bash_profile
exec $SHELL

### pyenv-virtualenv
<div>
</div>

#### Mac
<div>
</div><div>brew install pyenv-virtualenv</div><div>
</div><div>Add</div><div>eval "$(pyenv virtualenv-init -)"</div><div>to your profile (add it to ~/.bash_profile)

</div>

#### Others
<div>
</div><div><div># Install pyenv virtualenv</div><div>git clone https://github.com/yyuu/pyenv-virtualenv.git ~/.pyenv/plugins/pyenv-virtualenv</div><div>
</div><div># auto ativate virtualenv for pyenv</div><div>echo 'eval "$(pyenv virtualenv-init -)"' &gt;&gt; ~/.bash_profile</div><div>**Zsh note: Modify your ~/.zshenv file instead of ~/.bash_profile.**
**Ubuntu note: Modify your ~/.bashrc file instead of ~/.bash_profile.**
**
**</div><div># restart shell</div></div><div>exec $SHELL

</div>

## Usage
<div>
</div>

### pyenv
<div>
</div># install python
pyenv install 2.7.9
pyenv install 3.4.3

# if there are problems when install the python, you can refer to
#&nbsp;https://github.com/yyuu/pyenv/wiki/Common-build-problems

# rehash when install the new versions every time
pyenv rehash

# set version of python to use for this session
pyenv shell 3.4.3

# set global python for everytime we start pyenv
pyenv global 3.4.3

# set python version for current and all sub directories
pyenv local 3.4.3

### pyenv-virtualenv
<div>
</div>Restart the shell and let’s create an virtualenv with Python 2.7.8.
pyenv virtualenv 2.7.8 project-a-2.7.8

Activate the newly created virtualenv.
pyenv activate project-a-2.7.8

You can deactivate the current virtualenv.
pyenv deactivate

And list the available virtualenvs.
pyenv virtualenvs

Those virtualenvs are located in ~/.pyenv/versions just like those installed Pythons. If you want to remove a virtualenv, simply delete that corresponding folder.
Or
pyenv uninstall my-virtual-env

Reference:
http://eureka.ykyuen.info/2014/07/11/pyenv-python-version-manager/
http://eureka.ykyuen.info/2014/07/14/manage-your-python-projects-with-virtualenv/
http://blog.froehlichundfrei.de/2014/11/30/my-transition-to-python3-and-pyenv-goodby-virtualenvwrapper.html
https://godjango.com/96-django-and-python-3-how-to-setup-pyenv-for-multiple-pythons/
https://github.com/yyuu/pyenv
https://github.com/yyuu/pyenv-virtualenv
http://www.openfoundry.org/tw/tech-column/8516-pythons-virtual-environment-and-multi-version-programming-tools-virtualenv-and-pythonbrew