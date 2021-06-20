---
layout: post
title: "Machine Learning, Hung-yi Lee (NTU course 2020, Spring)"
subtitle: 
tags: [course, in progress]
comments: true
published: true
---

<!-- # Machine Learning, Hung-yi Lee (NTU course 2020, Spring)   -->

### [See Syllabus](http://speech.ee.ntu.edu.tw/~tlkagk/courses_ML20.html)

<img src="/assets/images/Machine Learning, Hung-yi Lee/ML_Learning_Map.png" style="vertical-align:middle;margin:0px 50px" width="80%">

### **Course List:**

- [x] Introduction of Machine Learning

- [ ] Regression 
- [x] Gradient Descent
- [x] Classification

    <!-- Deep Learning -->
- [x] Deep Learning, Backpropagation
- [x] CNN
- [x] RNN
- [x] Semi-supervised, Word Embedding 

    <!-- 前沿研究 -->
- [ ] Explainable AI
- [ ] Adversarial Attack  <!-- 加入雜訊的惡意攻擊 -->
- [ ] Network Compression  <!-- edge computable的問題 -->
    <!--  -->

- [ ] Auto-encoder
- [ ] Anomaly Detection
- [ ] GAN
- [ ] Transfer Learning (Domain Adversarial Learning) <!-- 訓練測試類似分布的假設，如何在少量、新的不一樣分布測試資料上調整模型 -->
- [ ] Meta Learning (MAML) (learn to learn, find proper functional space)
- [ ] Life-long Learning  <!-- task 1, task 2, task 3, ... continuous learning  -->
- [ ] Reinforcement Learning


----
## Notes

- [Introduction of Deep Learning](../ML_course/note_IntroductionDeepLearning/index.html)

- [Convolutional Neural Network](../ML_course/note_CNN/index.html)

- [Recurrent Neural Network](../ML_course/note_RNN/index.html)

- [Word Embedding](../ML_course/note_WordEmbedding/index.html)


<!-- ----
Supervised: tell machine what is next is better  
Reinforcement learning: define Reward to let machine keep  learning the better solution. Finallly, it will win like Alpha Go!  
Network architecture   -->


<!-- ----
##  Anomaly Detection
<img src="/assets/images/Machine Learning, Hung-yi Lee/anomalydetection_1.JPG" style="vertical-align:middle;margin:0px 50px" width="80%">


----
##  Attack ML Models
<img src="/assets/images/Machine Learning, Hung-yi Lee/anomalydetection_2.JPG" style="vertical-align:middle;margin:0px 50px" width="80%">

訓練好的ML model能夠:  

- 穩定性

- 應付來自資料面上千奇百怪的input

- 偵測**垃圾郵件、惡意軟體、網路入侵**


譬如現在有一張照片original image $A$, 我們將他pixel的值作平移 $(x_1, x_2, ... ) + (\delta_1, \delta_2,...)$ 得到 $A^{'}$

這裡 $A^{'}$即是一個對ML model攻擊的樣本。 -->