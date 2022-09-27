---
layout: page
title: "CNN: Age-gender Image Classification"
description: "The classification of images with CNN"
img: assets/img/3.jpg
importance: 2
category: Data Science & Machine Learning
---

### **Requirements**
This project is written in Python and requires the following libraries to be **installed** and **imported**. 

<script src="https://gist.github.com/mphamsy/e133b225d5e4814adfd9e18f70f30b63.js"></script>

The project is undertaken with GoogleColab due to GPU requirements with images stored locally.

<script src="https://gist.github.com/mphamsy/371650ed2089a2fd5a73285acf9b8a99.js"></script>

### **Dataset**
The dataset chosen for this project is a fraction of the UTKFace dataset containing facial images of people aged from 0 to 116 with resolution of 128x128. These types of datasets are important and widely used for computer vision tasks. This assignment will only use a fraction of the dataset, which will equate to 5000 images total. These images will be randomly split to training and testing datasets as follows:

- The training dataset size:  3500
- The testing dataset size: 1500

The information about gender, age and ethncity are encoded within each **filename**. The information is presented as following:

```
Sample Filename: 96_1_2_20170110175716420.jpg.chip.jpg
Encoded Meaning: Age_Gender_Ethnicity_Timestamp.jpg.chip.jpg
```

The visualisation of the dataset is provided below. 20 images are displayed with age and gender shown above each picture.

<script src="https://gist.github.com/mphamsy/36ebd8842e2e4ccfad3a1949370ffb20.js"></script>

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/cnnage.JPG" title="Example Data" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Sample images with age and gender captions
</div>
<br/>

### **Pre-processing**

The train and test images were stores inside respective train and test dataframes. The dataset was randomly split accordingly to dataset sizes proposed in the **Datatset** section.

<script src="https://gist.github.com/mphamsy/0b4902b9a06c3e0b784e5ae2188a6ce3.js"></script>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/agehist.JPG" title="Age histogram" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/genhist.JPG" title="Gender histogram" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

### **Data Augmentation**

<script src="https://gist.github.com/mphamsy/012e06c4f986a7154e491b3ab81ee25b.js"></script>

#### **Data Augmentation Results**

<script src="https://gist.github.com/mphamsy/2392c2cc81c6279ff490aa6085b0a5a1.js"></script>

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/aug.JPG" title="Data Augmentation" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The Data Augmentation results
</div>
<br/>
### **Convolutional Neural Network (CNN)**

Architecture:

<script src="https://gist.github.com/mphamsy/039c58a9c807297cf9f8a9175b08f61b.js"></script>

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/cnnarch.JPG" title="CNN architecture" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The CNN architecture
</div>
<br/>

### **Plots and Results**

<script src="https://gist.github.com/mphamsy/8105c3aa601c58ded307b15e5268a387.js"></script>

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/cnnlc.JPG" title="Lerning curves" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The learning curves
</div>
