---
layout: page
title: Question Generation from SQuAD dataset (ongoing)
description: 
img:
importance: 3
category: Deep Learning
---


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

<script src="https://gist.github.com/mphamsy/5cb70ca046058d4a7300ed0779ab01e1.js"></script>

### **Preprocessing**

### **Feature Conversion**

The dataset was sliced and only 26000 training and 5000 test samples were used during the training of the transformer.

### **Transformers**

### **Training**

### **Testing**

