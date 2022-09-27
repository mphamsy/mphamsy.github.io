---
layout: page
title: "SVM: Sentiment Classification"
description: "The sentiment review analysis utiliziting a support vector machine"
img: assets/img/movierev.JPG
importance: 1
category: Data Science & Machine Learning
---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/sentiment.JPG" title="sentiment" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<br/>

### **Requirements**
This project is written in Python and requires the following libraries to be **installed** and **imported**.

<script src="https://gist.github.com/mphamsy/47122ea0b84e2266ffb809d02c64e550.js"></script>
<br/>

### **Dataset**
The dataset chosen for this project is a fraction of the IMDB dataset containing 50k reviews for natural language processing (NLP) purposes. The dataset is devoted for binary classification tasks. Each review contains a corresponding negative or positive sentiment.
- The training dataset size:  5000
- The testing dataset size: 1500
The dataset is read and parsed with Pandas library. The sample example of the training dataset is shown in the figure below.

```
Sentiment: “Positive”
Review: “This little low-budget gem is thoroughly loveable and enjoyable and definitely a keeper. I give it an 11 out of 10!”
```
<br/>

### **Pre-processing**
The custom tokenizer function is created to handle the following aspects of each review.
-	Make all text lower case
-	Remove special punctuation and numerical values
-	Remove additional characters
-	Remove stop words
-	Stem remaining words with a snowball stemmer.

<script src="https://gist.github.com/mphamsy/0f9b39a0895e7df9b0ada44132bb6f89.js"></script>

Consequently, the tokenizer function is used inside the vectorizer function as a tokenizer input. The data itself requires to be vectorized to be processable for the SVM classifier.  The **Term Frequency Inverse Document Frequency (TF-IDF)** vectoriser is implemented that takes into consideration the commonality/frequency of words and weigh them accordingly. 

<script src="https://gist.github.com/mphamsy/e196f83c65dbadea36415bb13a867f07.js"></script>
<br/>

### **SVM Classifier**

A **Support Vector Machine (SVM)** is a supervised Machine Learning algorithm that performs well for text classification tasks. 

The SVM algorithms attempts to find the optimum hyperplane to divide n-dimensional data. This method works well for data that can be separated linearly. However, the majority of real-world problems are nonlinear. As a result, kernels are being utilized to convert linearly inseparable problems data into a higher-dimensional space, allowing the data to be linearly separable. 

The GridSearchCV utilizing **Scikit-learn** library will be used to find the optimal set of hyperparameters of C and gamma for the **sigmoid** kernel. The kernel choice optimization has been undertaken as a part of this project, and **sigmoid** kernel was found to be the best out of **RBH** and **Linear** kernels.

<script src="https://gist.github.com/mphamsy/335110934b18db63029229f2170ed333.js"></script>

```
Fitting 5 folds for each of 60 candidates, totalling 300 fits
[CV 1/5] END .C=0.1, gamma=0.01, kernel=sigmoid;, score=0.507 total time=   8.1s
[CV 2/5] END .C=0.1, gamma=0.01, kernel=sigmoid;, score=0.507 total time=   8.1s
[CV 3/5] END .C=0.1, gamma=0.01, kernel=sigmoid;, score=0.505 total time=   8.1s
[CV 4/5] END .C=0.1, gamma=0.01, kernel=sigmoid;, score=0.505 total time=   8.1s
[CV 5/5] END .C=0.1, gamma=0.01, kernel=sigmoid;, score=0.505 total time=   8.1s
...
[CV 4/5] END C=100.0, gamma=1.0, kernel=sigmoid;, score=0.775 total time=   8.1s
[CV 5/5] END C=100.0, gamma=1.0, kernel=sigmoid;, score=0.800 total time=   6.4s

The best parameters for sigmoid are: {'C': 0.4, 'gamma': 1.0, 'kernel': 'sigmoid'}
```

Based on the GridSearchCV finding the best hyperparameters of C and gamma are C: 0.4 and gamma: 1.0 for sigmoid kernel. The results of each hyperparameter pair of C and gamma based on the mean test score are displayed in the heatmap below.

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/SVMheatmap.JPG" title="Heatmap" class="middle" %}
    </div>
</div>
<div class="caption">
    The hyperparameter heatmap
</div>
<br/>

### **Training The Best Sigmoid SVM**
The SVM classifier is trained with the best parameters found from the GridSearchCV. The learning curves of the SVM model were recorded during the training of the best model.

<script src="https://gist.github.com/mphamsy/4634d9d8313d6bb3b620224dcfbf3aa9.js"></script>
```
The accuracy score is : 87.06%
```
The **accuracy score of 87.06%** was achieved for the best sigmoid kernel with its learning curves being displayed below.

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/LearningcurvesSVM.JPG" title="Learning Curves" class="middle" %}
    </div>
</div>
<div class="caption">
    Learning Curves for the best sigmoid kernel
</div>
<br/>

### **Results**

The results are highly satisfactory proving that SVM sigmoid kernel is capable of classifying reviews with an exceptional accuracy score of 87.06% with a limited size of the training data. Additional, training examples along with increasing the size of vocabulary data from 2000 may prove to be beneficial for the binary classification tasks. The overall performance of the SVM classifier is displayed in the following confusion matrix. 

<script src="https://gist.github.com/mphamsy/13187488c21b0f5e8ba15c51066fc44a.js"></script>

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0-center">
        {% include figure.html path="assets/img/CMSVM.JPG" title="confusion" align = "middle" class="center" %}
    </div>
</div>
<div class="caption">
    Confusion Matrix
</div>
