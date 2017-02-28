---
title: mac brew pyenv import tkinter
tags:
  - python
date: 2016-07-28 22:46:00
---

I use the homebrew and the pyenv to install python.

When I want to import tkinter, there is a error message:
&nbsp; &nbsp; import _tkinter # If this fails your Python may not be configured for Tk
ImportError: No module named '_tkinter'

Solve:
<pre class="prettyprint">
pyenv uninstall 3.5.1
brew tap Homebrew/dupes
brew install tcl-tk
pyenv install 3.5.1
</pre>
If there is a "zipimport" error when installing the python, solve by "xcode-select --install".

Reference:
http://qiita.com/hokkun-k/items/223b1125b814621a0c0e