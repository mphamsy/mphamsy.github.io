---
layout: page
title: "CNN: Age-gender Image Classification"
description: 
img: assets/img/cnnim.JPG
importance: 2
category: Deep Learning
---

<div class="row">
    <div class="col-md-5 offset-md-3">
        {% include figure.html path="assets/img/cnnprof.JPG" title="Age-Gender Classification" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

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
<div class="caption">
    Age Frequency Histogram (Left) and                       Gender Frequency Histogram (Right)
</div>
<br/>
### **Data Augmentation**

**Data Augmentation** is commonly used for Computer Vision projects to synthetically increase the size of dataset by manipulating existing images. This is achieved through rotating, zooming, shearing, flipping and shifting the original picture.

The advantages of data augmentation include increasing the dataset and therefore allowing for **more training** as well as **preventing overfitting**. Data Augmentation is achieved by using  the **ImageDataGenerator** which considers rotation, shift, shear, zoom and flip hyperparameters.

<script src="https://gist.github.com/mphamsy/012e06c4f986a7154e491b3ab81ee25b.js"></script>

```
Train: Found 3500 validated image filenames.
Test: Found 1500 validated image filenames.
```

#### **Data Augmentation Results**

12 images displaying the data augmentation results are presented below. 

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

The input layer consisted of images each with size 128x128x3.

The first part of our model consisted of two blocks of Convolution-Relu-BatchNormalisation-MaxPooling layers of size 128x128x8 and 64x64x16, respectively. With the aim of these blocks being to extract low-level features such as edges between background and faces in the image.

**Gender branch:**
- The binary classification is a much easier task and should be linearly separable in a non-linear feature dimension space introduced by the Relu activation function.
- The gender branch contains two Convolution-Relu-BatchNormalisation-MaxPooling layers that produce feature maps of dimensions 32x32x32 and 16x16x64, respectively. The size is reduced further to 8x8x64 before flattening.
- Twohidden dense Relu layers of size 256 and 64 connected to a single neuron activated by sigmoid function. 25% dropout is used between these layers.

**Age branch:**
- The regression task for age estimation has proven to be more challenging, hence, to introduce higher order of non-linearity; more convolutional blocks to the age branch were added.
- The age branch consisted of 6 consecutive convolutional blocks. The feature maps outputted were of dimension 8x8x64 and were fed into two dense Relu layers with 25% dropout connected to a single neuron activated by a linear function.

**Architecture:**

<script src="https://gist.github.com/mphamsy/039c58a9c807297cf9f8a9175b08f61b.js"></script>

<div class="row">
    <div class="col">
        {% include figure.html path="assets/img/CNNmodel.JPG" title="CNN architecture" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The CNN architecture
</div>
<br/>

### **Training**

Once the architecture model was completed, the model was subsequently trained. The model was trained for 45 epochs with binary cross entropy loss for the gender classification and mean absolute error loss for the age estimatetion.

<script src="https://gist.github.com/mphamsy/e39d1fe4e4e46621dc5903b2a475de52.js"></script>

### **Plots and Results**

The model has achieved **88.08% accuracy and 7.12 MAE** for age gender estimation. The results are satisfactory considering a small training dataset size and short duration of the training.

The training curves were plotted, which show that **no-over or underfitting occurs** due to drop-outs and the data augmentation.

<script src="https://gist.github.com/mphamsy/8105c3aa601c58ded307b15e5268a387.js"></script>

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/cnnlc.JPG" title="Lerning curves" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The learning curves
</div>
