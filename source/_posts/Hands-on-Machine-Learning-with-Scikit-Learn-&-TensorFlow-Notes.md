---
title: Hands on Machine Learning with Scikit-Learn & TensorFlow Notes
tags: 
  - ml
  - python
date: 2017-04-15 18:11:39
---

這邊紀錄閱讀 Hands on Machine Learning with Scikit-Learn & TensorFlow 的筆記。

# Ch 1: The Machine Learning Landscape

機器學習是一種讓電腦從資料中學習的方法。

問題過於複雜（long lists of rules）且需要不斷找到新的pattern，或者是難以直接用傳統程式語言描述並解出的問題，就適合使用機器學習從資料中找出解法。
且透過機器學習的方法，人類也可以去檢視學習出來的模型，來得到該問題的相關知識。

根據機器學習的種類，可以分成：
1. Supervised / Unsupervised Learning ： 資料是否有標記解答
2. Batch and Online Learning ： Online為每筆資料進來，就會調整模型
3. Instance-Based Versus Model-Based Learning

這三大類可以交互組合。

<!-- more -->

# Ch 2: End-to-End Machine Learning Project

這一張使用dataset走過一次機器學習的流程，使用scikit-learn。
首先要先定義好問題，定義好量測效果的指標，這裡使用RMSE。

## 常用的觀察資料方法
category feature可以用value_counts()查看
```python
housing["ocean_proximity"]. value_counts()
```

將資料中所有numerical屬性畫出histogram
```python
housing.hist( bins = 50, figsize =( 20,15))
```
會觀察到很多屬性會是tail-heavy，這種分布對於某些機器學習方法不甚理想，因此最好能將其轉換成bell-shaped distributions。

## 建置test set
一般人建置test set可能就是隨機抽樣，會有兩個問題。

### 第一個
當下次有新資料進來時，這次抽到的test set，有些可能上次是被分到train set。最理想是能維持一致性，上次是test set，這一次也仍在test set。

書中提出的方法為，為每一筆資料編號一個獨特的ID，並每次切分train/test set時，使用同樣的順序或邏輯。比如若將每個屬性相加hash過後的值當作ID，那麼可以將hash後個位數值大於等於8者當作test set，如此因每次hash後值會一樣，每次都會分到相同的set。

比較一般的做法，仍是使用隨機抽樣的方法，只是要保證每次資料的順序一致，且鎖定random seed，此種做法可以使用scikit-learn的**train_test_split**函數。

### 第二個
假若資料的分佈實際上有某中趨勢，但是我們仍使用隨機抽樣的方式，此時test set會與實際資料產生抽樣上的誤差。比如資料男女的分配比率為60比40，使用隨機抽樣的男女分配比例，會很難接近這樣的比例，有較大誤差。需使用**stratified sampling**。

而在書中實際運用的例子為，median income的屬性對於房價的預估很重要，希望這個屬性盡量趨近正確的分佈。但因此屬性為連續的數值，所以須先將其切分bin轉成category來使用。在切bin時要注意，每個bin都要有足夠的sample數量，如此才可做stratified sampling。

可以使用scikit-learn的**StratifiedShuffleSplit**或者**train_test_split**也有一個**stratify**參數可以設定。

## 觀察資料
不觀察test set，且若training set資料量過大，可以另外sample出小一點的set來觀察。

畫scatter plot
```python
housing.plot( kind =" scatter", x =" longitude", y =" latitude", alpha = 0.4, s = housing[" population"]/ 100, label =" population", c =" median_house_value", cmap = plt.get_cmap(" jet"), colorbar = True, )
```

計算standard correlation coefficient (also called Pearson’s r)
```python
corr_matrix = housing.corr()
corr_matrix[" median_house_value"]. sort_values( ascending = False)
```
0代表無關聯，1或-1代表有極度關聯。但是此僅能表示線性關聯。

使用pandas的scatter_matrix，繪製所有**數值**屬性倆倆的scatter chart。挑出需要看關係的屬性即可，否則會太多圖。
```python
from pandas.tools.plotting import scatter_matrix 
attributes = [" median_house_value", "median_income", "total_rooms", "housing_median_age"] 
scatter_matrix( housing[ attributes], figsize =( 12, 8))
```
除了觀察資料外，還有一個重點是做feature engineering，將不同的屬性用不一樣的方式結合成新的屬性，很有可能原先的屬性沒有效果，結合後變得很有效果。

## 準備資料

### Missing Values
大多數的方法無法處理missing values，有三種方式處理
1. 將有missing value的row拿掉
2. 將有missing value的屬性拿掉
3. 用某種方法填充missing value（比如中位數）

若使用第三種方法，如計算中位數記得僅使用training set data。然後再將其值填充到training/test set。

**Imputer**為scikit-learn提供處理missing values的class，它只能處理數值屬性，因此使用它處理時，記得把非數值屬性先drop掉。
```python
from sklearn.preprocessing import Imputer 
imputer = Imputer( strategy =" median")
housing_num = housing.drop(" ocean_proximity", axis = 1) #丟掉非數值屬性
imputer.fit( housing_num)
imputer.statistics_ #查看計算出的結果
X = imputer.transform( housing_num)
housing_tr = pd.DataFrame( X, columns = housing_num.columns) #可以這樣轉回pandas
```

### Non-numerical Attributes
多數方法喜歡數值型態的屬性


# Ch 6: Decision Trees

Decision使用Gini來衡量乾淨程度（最後所有的sample都能分到正確的class）
\\[G_{i} = 1 - \sum_{k=1}^{n}p_{i,k}^{2}\\]
p代表在該節點中該類別所佔之比例。

![](http://i.imgur.com/C8AGVQX.png)
如圖中的綠色，其Gini為\\(1-(0/54)^2-(49/54)^2-(5/54)^2=0.168\\)。
