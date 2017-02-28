---
title: learn machine learning
tags:
  - ml
date: 2016-02-23 20:22:00
---

<span class="inline_editor_value"><span class="rendered_qtext">From:&nbsp; https://www.quora.com/Machine-Learning/How-do-I-learn-machine-learning-1</span></span>

<span class="inline_editor_value"><span class="rendered_qtext">I didn't  do a PhD on machine learning (was mostly focused on Signal Processing  and Software Engineering) so I get this question a lot. The typical  person that asks me this question is a software engineer with a computer  science background, so I will address it from that perspective. If you  are a Math major, for example, my answer might be less useful.

The first thing I tell someone who wants to get into machine learning is to take Andrew Ng's <span class="qlink_container">[online course](https://www.coursera.org/course/ml)</span>.  I think Ng's course is very much to-the-point and very well organized,  so it is a great introduction for someone wanting to get into ML. I am  surprised when people tell me the course is "too basic" or "too  superficial". If they tell me that I ask them to explain the difference  between Logistic Regression and Linear Kernel SVMs, PCA vs. Matrix  Factorization, regularization, or gradient descent. I have interviewed  candidates who claimed years of ML experience that did not know the  answer to these questions. They are all clearly explained in Ng's  course. There are other online courses you can take after this one such  as <span class="qlink_container">[](https://www.coursera.org/course/mmds)</span></span></span>
<div class="tooltip" style="display: block; left: -16px; top: -31px;"><div class="tooltip_contents nub_bottom">[<span>coursera.org</span>](https://www.coursera.org/course/mmds)</div></div>[Mining Massive Datasets](https://www.coursera.org/course/mmds) or <span class="qlink_container">[Recommender Systems](https://www.coursera.org/learn/recommender-systems)</span>, but at this point you are mostly ready to go to the next step.

<span class="inline_editor_value"><span class="rendered_qtext">My  recommended next step is the following. Get a good ML book (my list  below), read the first intro chapters, and then jump to whatever chapter  includes an algorithm you are interested. Once you have found that  algo, dive into it, understand all the details, and, especially,  implement it. In the previous online course you would already have  implemented some algorithms in Octave. But, here I am talking about  implementing an algorithm from scratch in a "real" programming language.  You can still start with an easy one such as L2-regularized Logistic  Regression, or k-means, but you should also push yourself to implement  more interesting ones such as LDA (Latent Dirichlet Allocation) or SVMs.  You can use a reference implementation in one of the many existing  libraries to make sure you are getting comparable results, but ideally  you don't want to look at the code but actually force yourself to  implement it directly from the mathematical formulation in the book.

So, what are some good books to do this? Many have been mentioned before. Some of my favorite:</span></span>

*   Hastie, Tibshirani, and Friedman's <span class="qlink_container">[The Elements of Statistical Learning](http://statweb.stanford.edu/%7Etibs/ElemStatLearn/)</span>
*   Bishop's <span class="qlink_container">[Pattern Recognition and Machine Learning](http://research.microsoft.com/en-us/um/people/cmbishop/prml/)</span>*   David Barber's <span class="qlink_container">[Bayesian Reasoning and Machine Learning](http://web4.cs.ucl.ac.uk/staff/D.Barber/pmwiki/pmwiki.php?n=Brml.HomePage)</span>
*   Kevin Murphy's <span class="qlink_container">[Machine learning: a Probabilistic Perspective](http://www.cs.ubc.ca/%7Emurphyk/MLbook/)</span>You can also go directly to a research paper that introduces an algorithm or approach you are interested on and dive into it.

My  main point is that machine learning is both about breadth as depth. You  are expected to know the basics of the most important algorithms (see  my answer to <span class="qlink_container">[ What are the top 10 data mining or machine learning algorithms?](https://www.quora.com/What-are-the-top-10-data-mining-or-machine-learning-algorithms/answer/Xavier-Amatriain)</span>).  On the other hand, you are also expected to understand low-level  complicated details of algorithms and their implementation details. I  think the approach I am describing addresses both these dimensions and I  have seen it work.

**Edit 08/26/2015**

In response to  some comments and questions, I feel that I should add another book  recommendation. If you feel like you lack some background in Statistics,  I would totally recommend:

*   Larry Wasserman's <span class="qlink_container">[All of Statistics: A Concise Course in Statistical Inference](http://www.amazon.com/All-Statistics-Statistical-Inference-Springer/dp/0387402721)</span>This  books cover all the topics in statistics that you need for  understanding ML concepts. As a matter of fact, the book itself has a  pretty good introduction to many of the typical ML approaches such as  regression and classification.