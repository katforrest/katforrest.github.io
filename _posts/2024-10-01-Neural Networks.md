---
layout: post
title: Neural Network Modeling
---

As part of my coursework in Advanced Learning Algoriths with Stanford Online, I experimented with different types of neural network models using tensorflow.  

My code and the dataset are available on [GitHub](https://github.com/katforrest/Statistics-Fundamentals).

This iris[^1] dataset is great for experimentation. This dataset classifies observations into one of three species of iris based on four features. Here is a quick visualization of the four features in this data. Clear patterns are immediately visible.
<div align="center">
  <img src="https://raw.githubusercontent.com/katforrest/katforrest.github.io/master/assets/img/Neural_Multi_iris_1.jpg" alt="Fig 1" width="80%">
</div>
I like to visualize my data by plotting just the first two features on an x y coordinate graph, using different shapes to represent the different classes. While this doesn’t give me a complete picture, it does allow me to quickly see if there are clear linear boundaries between classes. Both visualizations tell me that there are clear and strong correlations between the features and the target classifications. 
<div align="center">
  <img src="https://raw.githubusercontent.com/katforrest/katforrest.github.io/master/assets/img/Neural_Multi_iris_2.jpg" alt="Fig 2" width="50%">
</div>

For the iris dataset, I created a multiclass classification model with a softmax output layer activation. When using a softmax activation, the output layer must have the same number of neurons as there are classes. In this case, there were three species of iris, so my output layer had three activations.  
The softmax layer calculates three scores for each observation. Each one represents the probability that the observation is one of the three species of iris. I use another function after I get my results to determine, out of the three, which type of iris the specimen is most likely to be.  
The first thing I do with my results is to plot the first two features and compare the predictions with the actual data. They look nearly identical!
<div align="center">
  <img src="https://raw.githubusercontent.com/katforrest/katforrest.github.io/master/assets/img/Neural_Multi_iris_3.jpg" alt="Fig 3" width="90%">
</div>
I also plot a confusion matrix, using the scikit-learn library, to visualize my results. The center diagonal made up of the darkest squares represents the true positives from my model. 
<div align="center">
  <img src="https://raw.githubusercontent.com/katforrest/katforrest.github.io/master/assets/img/Neural_Multi_iris_4.jpg" alt="Fig 4" width="50%">
</div>
This model was immediately highly accurate; it achieved an F1 score of 97% immediately, with no need for parameter adjustments to optimize the model.

In my conclusions, I noted that the iris data is highly predictable. Despite being a small dataset (only 150 observations), it has strong, clear patterns with minimal noise. There are almost no outliers or anomalies. The classes are easily separated with a linear boundary, which is evident in my first two visualizations of the data. And there is little class imbalance; the three types of iris are pretty evenly represented. 

<br><br><br>
On the other hand, this wine quality data[^2] yielded much less satisfying results. This dataset of 1599 observations contains eleven features that each represent a different physicochemical attribute of red wines. Accuracy was challenging; there weren’t any clear patterns amongst the data. Additionally, the class imbalance is very high. Each observation is assigned a quality score on a scale of 1 - 10, but the majority of the wines fall in the 5 and 6 range.

My first model is a binary classification model, or a logistic regression model. For this model, I picked an arbitrary quality score to use as the threshold value for a binary classification. Everything with a score of 6 or above is considered a "Quality Wine" or “1”. I updated the dataset to reflect this criteria and trained the model to distinguish between a "quality wine" and a "not quality wine."
<div align="center">
  <img src="https://raw.githubusercontent.com/katforrest/katforrest.github.io/master/assets/img/Neural_Logistic_wine_1.jpg" alt="Fig 4" width="50%">
</div>
A quick visualization of the first four features shows us no clear correlations between the feature characteristics and the target 0 or 1 values. 
<div align="center">
  <img src="https://raw.githubusercontent.com/katforrest/katforrest.github.io/master/assets/img/Neural_Logistic_wine_2.jpg" alt="Fig 4" width="50%">
</div>
I've tested this dataset before using a simple logistic regression model with a gradient descent algorithm that I implemented from scratch. The results were largely inaccurate. This model had an F1 score of 33%
<div align="center">
  <img src="https://raw.githubusercontent.com/katforrest/katforrest.github.io/master/assets/img/Neural_Simple_wine_1.jpg" alt="Fig 4" width="50%">
</div>

[^1]: Fisher, R. A.. 1936. Iris. UCI Machine Learning Repository. https://doi.org/10.24432/C56C76.
[^2]: Cortez, Paulo, A. Cerdeira, F. Almeida, T. Matos, and J. Reis. 2009. Wine Quality. UCI Machine Learning Repository. https://doi.org/10.24432/C56S3T.
