---
title: Hands on Machine Learning with Scikit-Learn & TensorFlow Notes
tags: 
  - ml
  - python
date: 2017-04-15 18:11:39
---

這邊紀錄閱讀 Hands on Machine Learning with Scikit-Learn & TensorFlow 的筆記。

## Ch 1: The Machine Learning Landscape

機器學習是一種讓電腦從資料中學習的方法。

問題過於複雜（long lists of rules）且需要不斷找到新的pattern，或者是難以直接用傳統程式語言描述並解出的問題，就適合使用機器學習從資料中找出解法。
且透過機器學習的方法，人類也可以去檢視學習出來的模型，來得到該問題的相關知識。

根據機器學習的種類，可以分成：
1. Supervised / Unsupervised Learning ： 資料是否有標記解答
2. Batch and Online Learning ： Online為每筆資料進來，就會調整模型
3. Instance-Based Versus Model-Based Learning
這三大類可以互相交互組合。

<!-- more -->

## Ch 2: End-to-End Machine Learning Project

這一張使用dataset走過一次機器學習的流程，使用scikit-learn。
首先要先定義好問題，定義好量測效果的指標，這裡使用RMSE。

### 常用的觀察資料方法
category feature可以用value_counts()查看
```python
housing["ocean_proximity"]. value_counts()
```

將資料中所有numerical屬性畫出histogram
```python
housing.hist( bins = 50, figsize =( 20,15))
```
會觀察到很多屬性會是tail-heavy，這種分布對於某些機器學習方法不甚理想，因此最好能將其轉換成bell-shaped distributions。

### 建置test set
一般人建置test set可能就是隨機抽樣，會有兩個問題。

第一個
