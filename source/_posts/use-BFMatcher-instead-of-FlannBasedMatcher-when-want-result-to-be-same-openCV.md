---
title: >-
  use BFMatcher instead of FlannBasedMatcher when want result to be same
  (openCV)
tags:
  - opencv
date: 2015-05-09 01:02:00
---

FlannBasedMatcher is a <span style="color: red;">approximate </span>matcher, and in my opinion it is depend on some random number.
Therefore if the execution sequence is the same, the result will be same.
However, this will lead to the result that when the same thing do twice, the result will not be the same.

So if we want to guarantee the result will be <span style="color: red;">same no matter do it at any time</span>, we should use <span style="color: red;">BFMatcher</span>.