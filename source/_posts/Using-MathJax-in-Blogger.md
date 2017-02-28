---
title: Using MathJax in Blogger
tags:
  - blogger
date: 2014-10-25 23:33:00
---

It's really easy. Just add the following code above &lt;head&gt; in blogger's template: 
<pre class="brush: html">&lt;script type="text/javascript"
  src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"&gt;
&lt;/script&gt;
</pre>
And you can test it now! 
\(          J_\alpha(x) = \sum\limits_{m=0}^\infty \frac{(-1)^m}{m! \, \Gamma(m + \alpha + 1)}{\bigl({\frac{x}{2}}\bigr)}^{2 m + \alpha} \) 
<pre>\(
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;J_\alpha(x) = \sum\limits_{m=0}^\infty \frac{(-1)^m}{m! \, \Gamma(m + \alpha + 1)}{\bigl({\frac{x}{2}}\bigr)}^{2 m + \alpha}

\)
</pre>