---
title: iOS Prefix.pch
tags: []
date: 2014-11-20 13:13:00
---

I meet a problem that Xcode success to build the project and run correctly.
But it show many syntax errors in the editor because of undefined type name.
That type is inside the class file that I include in the prefix.pch.

[http://stackoverflow.com/questions/24158648/why-isnt-projectname-prefix-pch-created-automatically-in-xcode-6](http://stackoverflow.com/questions/24158648/why-isnt-projectname-prefix-pch-created-automatically-in-xcode-6)

This is something I find with prefix.pch in Xcode 6\. 
I set the "Increase Sharing of Precompiled Headers" to "YES", then every thing get fine. 
That's weird.