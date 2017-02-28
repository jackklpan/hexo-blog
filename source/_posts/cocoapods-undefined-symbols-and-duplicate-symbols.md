---
title: cocoapods undefined symbols and duplicate symbols
tags:
  - cocoapods
  - ios
date: 2015-12-06 16:51:00
---

delete Pod directory, Podfile.lock, *.xcworkspace
Pod install

Edit Scheme (which is on the right of stop button) -&gt; Build -&gt; Add Pods before our project if the Pods not shown

Add origin project Search Path &amp; Other Linker Flags with $(inherited)

<span style="background-color: white; color: #222222; font-family: &quot;arial&quot; , &quot;helvetica neue&quot; , &quot;helvetica&quot; , sans-serif; font-size: 15px;">Change Build Active Architecture Only to No</span>
http://stackoverflow.com/questions/5303933/xcode4-linking-problem-file-was-built-for-archive-which-is-not-the-architecture