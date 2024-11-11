---
layout: post
title: Neural Network Modeling
---

As part of my coursework in Advanced Learning Algoriths with Stanford Online, I experimented with different types of neural network models using tensorflow.  

My code and the dataset are available on [GitHub](https://github.com/katforrest/Statistics-Fundamentals/tree/main/Neural%20Networks).

This iris[^1] dataset is great for experimentation. This dataset classifies observations into one of three species of iris based on four features. Here is a quick visualization of the four features in this data. Clear patterns are immediately visible.
<div align="center">
  <img src="https://raw.githubusercontent.com/katforrest/katforrest.github.io/master/assets/img/Neural_Multi_iris_1.jpg" alt="Fig 1" width="80%">
</div>
Before I start modeling, I like to visualize my data by plotting just the first two features on an x y coordinate graph, using different shapes to represent the different classes. While this doesn’t give me a complete picture, it does allow me to quickly see if there are clear linear boundaries between classes. Both visualizations tell me that there are clear and strong correlations between the features and the target classifications. 
<div align="center">
  <img src="https://raw.githubusercontent.com/katforrest/katforrest.github.io/master/assets/img/Neural_Multi_iris_2.jpg" alt="Fig 2" width="60%">
</div>

For the iris dataset, I created a multiclass classification model with a softmax output layer activation. When using a softmax activation, the output layer must have the same number of neurons as there are classes. In this case, there were three species of iris, so my output layer had three activations. The softmax layer calculates three scores for each observation. Each one represents the probability that the observation is one of the three species of iris. I use another function after I get my results to determine, out of the three, which type of iris the specimen is most likely to be.  
<br>
The first thing I do with my results is to plot the first two features and compare the predictions with the actual data. They look nearly identical!
<div align="center">
  <img src="https://raw.githubusercontent.com/katforrest/katforrest.github.io/master/assets/img/Neural_Multi_iris_3.jpg" alt="Fig 3" width="90%">
</div>
I also plot a confusion matrix, using the scikit-learn library, to visualize my results. The center diagonal made up of the darkest squares represents the true positives from my model. 
<div align="center">
  <img src="https://raw.githubusercontent.com/katforrest/katforrest.github.io/master/assets/img/Neural_Multi_iris_4.jpg" alt="Fig 4" width="60%">
</div>
This model was highly accurate; it achieved an F1 score of 97% immediately, with no need for parameter adjustments for optimization. 
<br>
In my conclusions, I noted that the iris data is highly predictable. Despite being a small dataset (only 150 observations), it has strong, clear patterns with minimal noise. There are almost no outliers or anomalies. The classes are easily separated with a linear boundary, which is evident in my first two visualizations of the data. And there is little class imbalance; the three types of iris are pretty evenly represented. 
<br><br>
<div align="center">
* * *
</div>
On the other hand, this wine quality data[^2] yielded much less satisfying results. This dataset of 1599 observations contains eleven features that each represent a different physicochemical attribute of red wines. Accuracy was challenging; there weren’t any clear patterns amongst the data. Additionally, the class imbalance is very high. Each observation is assigned a quality score on a scale of 1 - 10, but the majority of the wines fall in the 5 and 6 range.
<br>
My first model is a binary classification model, or a logistic regression model. For this model, I picked an arbitrary quality score to use as the threshold value for a binary classification. Everything with a score of 6 or above is considered a "Quality Wine" or “1”. I updated the dataset to reflect this criteria and trained the model to distinguish between a "quality wine" and a "not quality wine."
<div align="center">
  <img src="https://raw.githubusercontent.com/katforrest/katforrest.github.io/master/assets/img/Neural_Logistic_wine_1.jpg" alt="Fig 5" width="70%">
</div>
A quick visualization of the first four features shows us no clear correlations between the feature characteristics and the target 0 or 1 values. 
<div align="center">
  <img src="https://raw.githubusercontent.com/katforrest/katforrest.github.io/master/assets/img/Neural_Logistic_wine_2.jpg" alt="Fig 6" width="70%">
</div>
I've tested this dataset before using a simple logistic regression model with a gradient descent algorithm that I implemented from scratch. The results were largely inaccurate. This older model had an F1 score of 33%.
<div align="center">
  <img src="https://raw.githubusercontent.com/katforrest/katforrest.github.io/master/assets/img/Neural_Simple_wine_1.jpg" alt="Fig 7" width="60%">
</div>
I hoped that a neural network model would help solve the complexity in this data and perform much better. With so many features, I started with four layers. The first three use a relu activation type, and the output layer has a sigmoid activation. I arrived at this configuration with a lot of testing and adjustments. 
<br>
When training the model, the starting loss value was .6993. After 620 training epochs, the lowest loss value was .3979, which resulted in an F1 score of 71%. After 840 training epochs, the loss value was 0.3597, which resulted in an F1 score of 73%. At this point, it seemed like further adjustments to the model in terms of layers, neurons, training epochs or batch size was giving me diminishing returns. But 73% is still considerably better than my previous model that did not use a neural network, which had an F1 score of 33%. 
<br>
In this side by side comparison of the prediction to the validation data, it looks like the model performed reasonably well. 

<div align="center">
  <img src="https://raw.githubusercontent.com/katforrest/katforrest.github.io/master/assets/img/Neural_Logistic_wine_3.jpg" alt="Fig 8" width="80%">
</div>

The confusion matrix shows us the exact number of false positives, false negatives, and accurate predictions.
<div align="center">
  <img src="https://raw.githubusercontent.com/katforrest/katforrest.github.io/master/assets/img/Neural_Logistic_wine_4.jpg" alt="Fig 9" width="60%">
</div>

I also created a linear regression neural network model using the same wine quality dataset for comparison. I tried to control for the differences between the two as much as possible by using the same number of layers and neurons in both models. In my earlier model, I classified everything with a quality score of 6 or above as a "quality wine" or “1”. For this model, I left the quality score as is. Each wine in the dataset has a score on a scale of 1 - 10, with 10 being best quality. 

Here is a visualization of the different features and the corresponding quality score. While there are some patterns, there still isn’t any obvious linear separability between different quality scores.
<div align="center">
  <img src="https://raw.githubusercontent.com/katforrest/katforrest.github.io/master/assets/img/Neural_Linear_wine_1.jpg" alt="Fig 10" width="70%">
</div>
<div align="center">
  <img src="https://raw.githubusercontent.com/katforrest/katforrest.github.io/master/assets/img/Neural_Linear_wine_2.jpg" alt="Fig 11" width="70%">
</div>
I made several adjustments here to optimize performance. But the results were disappointing. The loss value started to decrease at a much slower rate very quickly. I ran nearly 2,000 training epochs, and only achieved an F1 score of 57% on the validation data.
<br>
For this model, I needed new ways to visualize my results and compare them with the actual observations. I tried plotting the real and predicted values for each feature, as seen here. The darker red values represent the predictions. But the results are not very clear. 
<div align="center">
  <img src="https://raw.githubusercontent.com/katforrest/katforrest.github.io/master/assets/img/Neural_Linear_wine_3.jpg" alt="Fig 12" width="70%">
</div>

A confusion matrix gives us much more information. We can see here that the data is highly imbalanced. The majority of observations have a quality score of either 5 or 6. Still, I was pleased to find that even when the prediction was incorrect, the score it assigned was only one point away from the actual value. It predicted a 6 for a wine that was actually a 5, for instance.
<div align="center">
  <img src="https://raw.githubusercontent.com/katforrest/katforrest.github.io/master/assets/img/Neural_Linear_wine_4.jpg" alt="Fig 13" width="60%">
</div>
I concluded that the F1 score and the other elements in the scikit-learn classification report were not the best methods for comparing the performance of my two models. While the logistic model results have more instances of accuracy, the linear model results still capture the general patterns in the data effectively. This is evident from the confusion matrix, where even incorrect predictions remained close to the true value, indicating a strong alignment with the overall pattern in the data.
<br>
The logistic model is also more forgiving. With a binary threshold of 0.5, the logistic model only needs to assign values broadly above or below this point. The exact value isn’t as critical as it is in the linear models. This allows the model to achieve high “accuracy” with less precise predictions. 
<br>
To normalize these differences, I converted the results of my linear regression model to a binary classification and ran the same metrics on the predictions. The resulting F1 score was identical in both models: 73%. The classification report below shows that there were only slight differences in precision and recall. Otherwise, the linear regression and binary classification performed equally well. 

<div align="center">
  <img src="https://raw.githubusercontent.com/katforrest/katforrest.github.io/master/assets/img/Neural_Linear_wine_5.jpg" alt="Fig 14" width="60%">
</div>
<div align="center">
  <img src="https://raw.githubusercontent.com/katforrest/katforrest.github.io/master/assets/img/Neural_Logistic_wine_5.jpg" alt="Fig 15" width="60%">
</div>

Overall, I’m pleased with the results from my experimentation. With these two datasets, I practiced implementing different types of neural networks. The differences in the types of regression and classification tasks led me to experiment with different visualizations and metrics for performance evaluation. I look forward to experimenting with new datasets and learning methods to further optimize classification and regression models. 



[^1]: Fisher, R. A.. 1936. Iris. UCI Machine Learning Repository. https://doi.org/10.24432/C56C76.
[^2]: Cortez, Paulo, A. Cerdeira, F. Almeida, T. Matos, and J. Reis. 2009. Wine Quality. UCI Machine Learning Repository. https://doi.org/10.24432/C56S3T.
