---
title: ie window open variable undefined
tags:
  - ie
date: 2016-08-08 16:02:00
---

Just like this problem
https://social.technet.microsoft.com/Forums/ie/en-US/466acbd2-9304-4714-9250-7669913d9a53/unable-to-pass-arguments-to-another-window-when-windowopen?forum=ieitprocurrentver

popupwindow = window.open();
popupwindow.a = "xxx";

However, in popupwindow, when use:
window.a shows "undefined"

This happened in IE, but work as expected in Chrome. (window.a shows "xxx" )

My workaround is:

window.a = "xxx";
popupwindow = window.open();

In popupwindow:
window.opener.a shows "xxx"