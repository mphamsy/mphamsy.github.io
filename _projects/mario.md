---
layout: page
title: "DDQN: Super Mario Bros"
description: "Super Mario Bros 1-1 World - Agent Reinforcement Learning with DDQN algorithm"
img: assets/img/7.jpg
importance: 3
category: Reinforcement Learning
---


### **Requirements**
This project is written in Python and requires the following libraries to be **installed** and **imported**. 
<script src="https://gist.github.com/mphamsy/4d92a28f58e7ad4efa2842fc757aa96c.js"></script>

### **Problem Definition**

In each stage of SMB, the player controls Mario's actions in order to avoid enemies and obstacles and eventually reach the flag pole that marks the end of a stage.  To allow systematic analysis on the interaction between Mario and the OpenAI Gym SMB environment, the game has been defined as a **Markov Decision Process (MDP)**, as illustrated shown in the figure below. 

At each time-step, Mario chooses an action and observes the reward of the action as well as the resulted new state.

### **Action and States**

States in SMB are represented as frame pixels of game scenes. Combinations of the locations of the stage map, Mario and monsters movements, and score bar changes would create new state representations. Resulting in an enormous state space that is prohibitive to compute using tabular methods. 

In SMB there are **12 possible actions**. Due to limited training time, the **‘RIGHT_ONLY’** set of actions has been chosen, where mario can only move and jump toward right. If more actions are given to Mario, it requires a larger amount of time to train. Mario has to use these actions to pass through the obstacles and reach the destination point.

### **Frames Preprocessing**

<script src="https://gist.github.com/mphamsy/76f7d90574949c6dc461561a75cfd5e1.js"></script>

### **CNN - Architecture**
In this project, we make use of the feature extraction capability of Convolutional Neural Network (CNN) to achieve such purpose
### **Mario - DDQN**

<script src="https://gist.github.com/mphamsy/ef16b972d1ab67883927432c39d02dff.js"></script>

### **Hyperparameters**

<script src="https://gist.github.com/mphamsy/e24819104e14a457fc88a8e45df7e981.js"></script>

### **Training**

<script src="https://gist.github.com/mphamsy/a5e821d0df38383744008110080e6e87.js"></script>

### **Results**

### **Post-training**

### **Takeaways and Conclusions**
