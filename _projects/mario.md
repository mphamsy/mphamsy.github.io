---
layout: page
title: "DDQN: Super Mario Bros"
description:
img: assets/img/marlog1.JPG
importance: 3
category: Reinforcement Learning
---
<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/marlog.JPG" title="SMB" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<br/>
### **Requirements**
This project is written in Python and requires the following libraries to be **installed** and **imported**. 
<script src="https://gist.github.com/mphamsy/4d92a28f58e7ad4efa2842fc757aa96c.js"></script>

### **Problem Definition**

In each stage of SMB, the player controls Mario's actions in order to avoid enemies and obstacles and eventually reach the flag pole that marks the end of a stage.  To allow systematic analysis on the interaction between Mario and the OpenAI Gym SMB environment, the game has been defined as a **Markov Decision Process (MDP)**, as illustrated shown in the figure below. 

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/marprob.JPG" title="SMB problem definition" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    SMB problem definition
</div>

At each time-step, Mario chooses an action and observes the reward of the action as well as the resulted new state.

### **Action and States**

States in SMB are represented as frame pixels. Combinations of the locations of the stage map, Mario and monsters movements, and score bar changes would create new state representations. Resulting in an enormous state space that is prohibitive to compute using tabular methods. 

In SMB there are **12 possible actions**. Due to limited training time, the **‘RIGHT_ONLY’** set of actions has been chosen, where mario can only move and jump toward right. If more actions are given to Mario, it requires a larger amount of time to train. Mario has to use these actions to pass through the obstacles and reach the destination point.

### **Frames Preprocessing**

Raw frames of the game are of size 240 x 256 x 3, which are computationally expensive to process. Therefore, all observations are converted into grayscale images with a resolution of 100 x 100. The frames are stacked in piles of 4 before being passed into the DDQN model, so that different motions can be represented. As SMB has a framerate of 60 fps, consecutive frames are likely to give similar information about the state, hence, only one in every 4 frames are used to avoid overlapping frames in the model.The preprocessing steps are illustrated in figure below.

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/marpre.JPG" title="SMB frames preprocessing" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    SMB frames preprocessing
</div>

<script src="https://gist.github.com/mphamsy/76f7d90574949c6dc461561a75cfd5e1.js"></script>

### **CNN - Architecture**
The DDQN will use of the feature extraction capability of Convolutional Neural Network (CNN). The model architecture is relatively small with no dropouts to avoid any information loss.

<script src="https://gist.github.com/mphamsy/06d5b5545a6153451266f3d59481b8ae.js"></script>

### **Mario - DDQN**

The main challenge in training a regular Deep Q-Network (DQN) is that there is no supervision. In the simple DQN implementation, both the target and current state-action Q-values are estimated using the same model. This leads to the correlation causing the shift, which inhibits the TD error from decreasing; which ultimately makes convergence of the model difficult.

One of the solutions is to use fixed targets, which are temporarily "frozen" in place - allowing for boosted convergence. A commonly used method introduces a second network (target net), which copies the weights of the DQN network (online net) after a number of steps in the environment. In this implementation, the variable controlling that is the update_steps.

Additionally, decoupling target Q-values from the online network helps preventing the overestimation of Q-values, which further improves training.

<script src="https://gist.github.com/mphamsy/ef16b972d1ab67883927432c39d02dff.js"></script>

### **Hyperparameters**

These are the hyper parameters used for the training of the Mario agent.

<script src="https://gist.github.com/mphamsy/e24819104e14a457fc88a8e45df7e981.js"></script>

### **Training**

Mario was trained for **2500 episodes** with hyperparameters used as show in the section Hyperparameters.

<script src="https://gist.github.com/mphamsy/a5e821d0df38383744008110080e6e87.js"></script>

### **Results**

The graph displays the agent reward performance over time. The agent continually learns throughout more episodes.

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/marlc.JPG" title="Mario learning curve" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Mario learning curve
</div>

### **Post-training**

The video following video shows the difference between agent at the beginning of the training and at the end.

<div class="video-container">
    <iframe width="672" height="378" src="https://www.youtube.com/embed/KxucJUMTmFY" title="Mario Agent" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
<br/>

### **Takeaways and Conclusions**

An issue seen throughout the training process was Mario’s tendency to get stuck behind obstacles, repeatedly running into them and failing to jump in order to clear them in the level’s time limit. By the end of training, Mario was able to deal with pipes, successfully identifying and jumping over them, but obstacles such as the stairs leading to the flag at the end of the level in 1-1 continued to be an issue. 

Mario also struggled with the first Piranha Plant enemy of the game - an enemy who emerges from pipes, preventing the player from jumping over (see figure below). By episode 2000, the agent was beating stage 1-1 in training, but very few runs saw Mario getting past this enemy. This is likely caused by the agent’s previous experience of pipes which can be safely jumped over - the Piranha Plant represents the an instance in the game where this is not the case.

<div class="row">
    <div class="col align-self-center">
        {% include figure.html path="assets/img/marlim.JPG" title="Mario limitations" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Mario limitations
</div>
