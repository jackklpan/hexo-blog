---
title: Using openCV SIFT in C++
tags: []
date: 2015-01-19 22:29:00
---

1\. 
<pre class="brush: cpp">
#include &ltopencv2\nonfree\features2d.hpp&gt
#include &ltopencv2\nonfree\nonfree.hpp&gt
</pre>
2\. link opencv_nonfree247.lib (247 is your opencv version) 
3\.  <pre class="brush: cpp">
initModule_nonfree();

Ptr&ltcv::FeatureDetector&gt detector = FeatureDetector::create("SIFT"); 
Ptr&ltcv::DescriptorExtractor&gt descriptor = DescriptorExtractor::create("SIFT"); 

// detect keypoints
std::vector&ltKeyPoint&gt keypoints1;
detector->detect(img1, keypoints1);

// extract features
Mat desc1, desc2;
descriptor->compute(img1, keypoints1, desc1);
</pre>