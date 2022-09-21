---
layout: page
permalink: /publications/
title: Publications
description: Works published by the Author.
nav: true
nav_order: 5
---

#### **Master's Thesis: Comparison of preprocessing strategies of Text-to-Text Transfer Transformer for Question Generation** 

##### **Executive Summary:**

Smart automatic question generation (AQG) reduces the strain on teachers and tutors to reproduce assessments on the annual basis as a part of intelligent tutoring systems (ITS). Traditionally, AQG suffered from scalability issues for rule-based systems or could not contextualize well as in the case of recurrent neural question generation (NQG). However, the recent advancements in deep learning in the form of pre-trained transformers can produce solid AQG frameworks on large knowledge domains.

This document undertakes the optimization of the state-of-the-art Text-to-Text Transfer Transformer (T5) to generate robust answer-aware questions for ITS purposes. The research looks into performances of prepending, highlight and prepending formatting with sentence-extraction encodings for varying learning rates. The evaluation includes standard n-gram metrics, semantic analysis, implementation of a question paraphraser and a question-answering (QA) model to further classify generated questions.

As all models were generating only one question per paragraph, they scored quite poorly in the evaluation with n-gram metrics. The paraphraser improved the n-gram performance of all models indicating that generated questions were similar to the rephrased references. The models proved to be robust with semantically generated questions that were contextually correct based on the findings from the QA framework.

**Key Words:** Automatic Question Generation (AQG), Intelligent Tutoring Systems (ITS), Text-to-Text Transfer Transformer (T5)
