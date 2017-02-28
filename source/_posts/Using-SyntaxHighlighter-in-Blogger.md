---
title: Using SyntaxHighlighter in Blogger
tags:
  - blogger
date: 2014-10-25 23:23:00
---

I use the Google Code Prettify Now.
[https://amobiz.github.io/2013/05/28/blogger-google-code-prettify-github-gist/](https://amobiz.github.io/2013/05/28/blogger-google-code-prettify-github-gist/)
[https://github.com/google/code-prettify/](https://github.com/google/code-prettify/)
Use method:
&lt;pre class="prettyprint"&gt;&lt;/pre&gt;

Add the following code above the &lt;head&gt; in your blogger's template: 
<pre class="brush: html">&lt;link href="http://alexgorbatchev.com/pub/sh/current/styles/shCore.css" rel="stylesheet" type="text/css"&gt;&lt;/link&gt; 
&lt;!-- the theme can change --&gt;
&lt;link href="http://alexgorbatchev.com/pub/sh/current/styles/shThemeDefault.css" rel="stylesheet" type="text/css"&gt;&lt;/link&gt; 
&lt;script src="http://alexgorbatchev.com/pub/sh/current/scripts/shCore.js" type="text/javascript"&gt;&lt;/script&gt; 
&lt;script src="http://alexgorbatchev.com/pub/sh/current/scripts/shBrushCpp.js" type="text/javascript"&gt;&lt;/script&gt; 
&lt;script src="http://alexgorbatchev.com/pub/sh/current/scripts/shBrushCSharp.js" type="text/javascript"&gt;&lt;/script&gt; 
&lt;script src="http://alexgorbatchev.com/pub/sh/current/scripts/shBrushCss.js" type="text/javascript"&gt;&lt;/script&gt; 
&lt;script src="http://alexgorbatchev.com/pub/sh/current/scripts/shBrushJava.js" type="text/javascript"&gt;&lt;/script&gt; 
&lt;script src="http://alexgorbatchev.com/pub/sh/current/scripts/shBrushJScript.js" type="text/javascript"&gt;&lt;/script&gt; 
&lt;script src="http://alexgorbatchev.com/pub/sh/current/scripts/shBrushPhp.js" type="text/javascript"&gt;&lt;/script&gt; 
&lt;script src="http://alexgorbatchev.com/pub/sh/current/scripts/shBrushPython.js" type="text/javascript"&gt;&lt;/script&gt; 
&lt;script src="http://alexgorbatchev.com/pub/sh/current/scripts/shBrushRuby.js" type="text/javascript"&gt;&lt;/script&gt; 
&lt;script src="http://alexgorbatchev.com/pub/sh/current/scripts/shBrushSql.js" type="text/javascript"&gt;&lt;/script&gt; 
&lt;script src="http://alexgorbatchev.com/pub/sh/current/scripts/shBrushVb.js" type="text/javascript"&gt;&lt;/script&gt; 
&lt;script src="http://alexgorbatchev.com/pub/sh/current/scripts/shBrushXml.js" type="text/javascript"&gt;&lt;/script&gt; 
&lt;script src="http://alexgorbatchev.com/pub/sh/current/scripts/shBrushPerl.js" type="text/javascript"&gt;&lt;/script&gt; 
&lt;script language="javascript"&gt; 
SyntaxHighlighter.config.bloggerMode = true;  //need to add this if we use blogger
SyntaxHighlighter.all();
&lt;/script&gt;
</pre>And one thing need to note is that if you want to add some code with &lt; or &gt;, you need to encode the code first. For example, you can use: [http://www.opinionatedgeek.com/dotnet/tools/htmlencode/encode.aspx](http://www.opinionatedgeek.com/dotnet/tools/htmlencode/encode.aspx)

Reference:
[http://alexgorbatchev.com/SyntaxHighlighter/](http://alexgorbatchev.com/SyntaxHighlighter/)
[http://www.craftyfella.com/2010/01/syntax-highlighting-with-blogger-engine.html](http://www.craftyfella.com/2010/01/syntax-highlighting-with-blogger-engine.html)