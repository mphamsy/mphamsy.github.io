---
layout: page
title: SVM: Sentiment Classification
description: The sentiment review analysis utiliziting a support vector machine
img: assets/img/12.jpg
importance: 1
category: Data Science & Machine Learning
---

To give your project a background in the portfolio page, just add the img tag to the front matter like so:

    ---
    layout: page
    title: project
    description: a project with a background image
    img: /assets/img/12.jpg
    ---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/1.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/3.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Caption photos easily. On the left, a road goes through a tunnel. Middle, leaves artistically fall in a hipster photoshoot. Right, in another hipster photoshoot, a lumberjack grasps a handful of pine needles.
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    This image can also have a caption. It's like magic.
</div>

You can also put regular text between your rows of images.
Say you wanted to write a little bit about your project before you posted the rest of the images.
You describe how you toiled, sweated, *bled* for your project, and then... you reveal its glory in the next row of images.


<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.html path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>


The code is simple.
Just wrap your images with `<div class="col-sm">` and place them inside `<div class="row">` (read more about the <a href="https://getbootstrap.com/docs/4.4/layout/grid/">Bootstrap Grid</a> system).
To make images responsive, add `img-fluid` class to each; for rounded corners and shadows use `rounded` and `z-depth-1` classes.
Here's the code for the last row of images above: a

### **Requirements**
This project is written in Python and requires the following libraries to be **installed** and **imported**.

<script src="https://gist.github.com/mphamsy/47122ea0b84e2266ffb809d02c64e550.js"></script>
<br/><br/>

### **Dataset**
The dataset chosen for this project is a fraction of the IMDB dataset containing 50k reviews for natural language processing (NLP) purposes. The dataset is devoted for binary classification tasks. Each review contains a corresponding negative or positive sentiment.
- **The training dataset size: ** 5000
- **The testing dataset size: ** 1500
The dataset is read and parsed with Pandas library. The sample example of the training dataset is shown in the figure below.

```
Sentiment: “Positive”
Review: “This film is not your typical Hollywood fare, though the pickings are so bad I often tend to stay away from movies rather than be disappointed. However, this little low-budget gem is thoroughly loveable and enjoyable and definitely a keeper. The actors are as varied as the characters they portray, the Buffalo setting is charming (what a pretty city), and the story sparkles. The lack of gratuitous violence, sex and the "f" word doesn't detract in the least! Take the kids, take grandma, take a break from Hollywood! I give it an 11 out of 10!”
```
<br/><br/>

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
<br/><br/>

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

Image

### **Training The Best Sigmoid SVM**
The SVM classifier is trained with the best parameters found from the GridSearchCV.

<script src="https://gist.github.com/mphamsy/4634d9d8313d6bb3b620224dcfbf3aa9.js"></script>

### **Results**

<script src="https://gist.github.com/mphamsy/13187488c21b0f5e8ba15c51066fc44a.js"></script>

{% raw %}
```html
<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.html path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
```
{% endraw %}
