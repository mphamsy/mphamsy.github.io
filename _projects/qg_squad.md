---
layout: page
title: T5 Question Generation from SQuAD 
description: 
img: assets/img/qglog.jpg
importance: 3
category: Deep Learning
---

<div class="row">
    <div class="col-md-6 offset-md-3">
        {% include figure.html path="assets/img/qgmain.JPG" title="Question Generation" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

### **Problem Definition**

Written and online assessments are the core of examination processes for most educational institutions. The students are required to undertake exams every year with an ever-changing curriculum, which puts a significant strain on tutors and teachers who are responsible for producing and generating the assessments on the annual basis. To tackle this issue, the concept of intelligent tutoring systems (ITS) is being explored.

Intelligent tutoring systems can create a substantial quantity of educational resources through the implementation of a large-scale and multi-domain knowledge base.The technological advance and availability of digital data sources resulted in the exploration of **automatic question generation (AQG)** as the potential alternative to manual question generation (QG) for ITS.

### **Answer-aware and answer-agnostic models**
Deep neural networks are used to generate questions from a given passage in a process known as neural question generation (NQG). The NQG is split into two categories of **answer-aware** and **answer-unaware** model types. In answer-aware models, both context and corresponding answer are supplied to generate a question, whereas answer-unaware models are only given the context.

As of now, **state-of-the-art (SOTA) systems are answer-aware** NQG as these vastly outperform answer-unaware and non-NQG approaches. Answer-aware models tend to generate better contextually and syntactically sound questions and therefore will be more suitable for QG tasks in the context of intelligent tutoring systems.

### **Requirements**
This project is written in Python and requires the following libraries to be **installed** and **imported**. 

<script src="https://gist.github.com/mphamsy/c1b0a6abaa68ac2ccfe1ac13b10c7d22.js"></script>

### **Dataset**

The source of question-generation data is the one provided by **Stanford Question Answering Dataset (SQuAD)** version 1. **SQuAD_v1** is a large-scale reading comprehension dataset consisting of approximately 98 thousand text paragraphs from Wikipedia, each supplemented with a complementary ground truth question and corresponding answer. Additionally, the dataset highlights individually answer locations within each paragraph. Figure below represents a random sample from the dataset.

<script src="https://gist.github.com/mphamsy/7bb405b5b921933b76c5043e8d541a3a.js"></script>

```
Length of the training dataset:  87599
Length of the validation dataset:  10570
```

The dataset overall contains parapgraph id, context, question, answer and answer starts. The DataFrame table was parsed, and paragraph ids was removed. The visualisation of the data is provided below.

<div class="row">
    <div class="col">
        {% include figure.html path="assets/img/qgdata.JPG" title="Squad dataset" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Example of the content inside the SQuAD Dataset 
</div>
<br/>
### **Preprocessing**

All QG pre-processing strategies are answer-aware systems, where both answer and context are used together as a text string input to train the model. The formats of train and test datasets were revised according to each of the pre-processing strategies and were later used in the post-processing for corresponding methods to generate questions.

The pre-processing strategy input consists of an answer followed by a context. The answer is separated from the context by a designated <SEP> token responsible for separating two various sentences in the same text string input.
  
  ```
  Prepending Encoder Input = Answer + <SEP> + Context
  ```
<div class="row">
    <div class="col">
        {% include figure.html path="assets/img/qgprep.JPG" title="Prepending Formatting" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The prepending formatting
</div>
  
<script src="https://gist.github.com/mphamsy/836bbaa7e57f7b2d962662d5a9ddf41c.js"></script>

### **Transformers**
  
The Text-to-Text Transfer Transformer (T5) is a completely text to text transformer proposed by Raffel et al. 2020. The T5 unifies NLP frameworks including question generation, summarization, sentiment analysis, language modelling, question answering or span extraction. Most importantly, T5 as a text-to-text frame can apply the same model, goal, training steps and decoding to every required task.
  
The T5 was trained on the Colossal Clean Crawled Corpus (C4), a dataset consisting of 750GB of cleaned and parsed English text taken from the web. Due to a sheer number of parameters taken into consideration while training, the T5 model has 5 size types, each with varying architecture to accommodate for parameter processing. T5-base type will be used to generate questions.
  
<div class="row">
    <div class="col">
        {% include figure.html path="assets/img/qgarch.JPG" title="T5 Architecture" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    T5 Architecture
</div>

<script src="https://gist.github.com/mphamsy/21a38d49c08c6821c63ed1ff2fee10d3.js"></script>

### **Feature Conversion**

The data was subsequently converted to features, collated and fed to the transformer T5.    
    
<script src="https://gist.github.com/mphamsy/3430b3e551fd75e1fac1304bf2c1c58f.js"></script>

<script src="https://gist.github.com/mphamsy/dab0427464b17f196f9b2312cf227b96.js"></script>

### **Training**
  
Following the feature conversion, the model can be trained. The dataset was sliced and only 26000 training and 5000 test samples were used during the training of the transformer for 7 epochs. All hyperparameters used can be seen in the following code. Note that the model is pushed onto HuggingFace, which requires an account to generate a write token to push the model to the hub. Otherwise, the model can be saved locally.

<script src="https://gist.github.com/mphamsy/2434244d1229f2a0e07ade46e5aa8eff.js"></script>

### **Testing**
  
The model was subsequently trained and pushed to the hub. The pre-trained t5 was then tested on context paragraphs and answer pairs to generate the questions.
  
<script src="https://gist.github.com/mphamsy/fc5514c1a6f095f02460a3158220158c.js"></script>
    
```
Answer + Context: four <sep> On January 7, 2012, Beyonce gave birth to her first child, a daughter, Blue Ivy Carter, at Lenox Hill Hospital in New York. Five months later, she performed for four nights at Revel Atlantic City's Ovation Hall to celebrate the resort's opening, her first performances since giving birth to Blue Ivy.
Actual: How many nights did Beyonce play at the resort?
Predicted: How many nights did Beyonce perform at the Ovation Hall?

Answer + Context: Bach and Mozart <sep> Chopin was educated in the tradition of Beethoven, Haydn, Mozart and Clementi; he used Clementi's piano method with his own students. He was also influenced by Hummel's development of virtuoso, yet Mozartian, piano technique. He cited Bach and Mozart as the two most important composers in shaping his musical outlook. Chopin's early works are in the style of the "brilliant" keyboard pieces of his era as exemplified by the works of Ignaz Moscheles, Friedrich Kalkbrenner, and others. Less direct in the earlier period are the influences of Polish folk music and of Italian opera.
Actual: Who did Chopin say were the two most important composers in his own music influences?
Predicted: Which two composers did Chopin consider the most important in his musical outlook?
    
Answer + Context: Zhu Yuanzhang <sep> In 1368, a Han Chinese revolt known as the Red Turban Rebellion toppled the Mongol Yuan dynasty in China. Zhu Yuanzhang then established the Ming dynasty, ruling as the Hongwu Emperor (r. 1368-1398). It is not clear how much the early Ming court understood the civil war going on in Tibet between rival religious sects, but the first emperor was anxious to avoid the same trouble that Tibet had caused for the Tang dynasty. 
Actual: Who created the Ming Dynasty? 
Predicted: Who established the Ming dynasty?
```

