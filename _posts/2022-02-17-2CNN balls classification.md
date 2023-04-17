---
tags: [CNN,Python,Google Colab]
---

# <a href="https://github.com/fd-col/Neural-network-balls-clasificacion">2CNN balls classification</a>
## Introduction
<p>The goal of this study was to create a simple CNN (Convolutional Neural Network) that could identify a specific dataset. </p>
<hr>
<p>The dataset has been choosen between those present on <a href="https://www.kaggle.com/">Kaggle</a>.

<p>Among all, 5 classes of these have been chosen: baseballs, basketballs, beach balls, billiard balls and bowling balls. In addition, some samples have been saved for verification.</p>

<img alt="Ball example" src="/assets/img/clasificador_bolas0.png" />
  
<p>  Data Augmentation had been applied to the orginal 110 elements for each class; the augmentation consist of rotating, changing lights to obtain new dataset elements. As a function of activation of neurons we used the RELU function which is: 
𝑟𝑒𝑙𝑢(𝑥) = 𝑥 · 𝑠𝑖𝑔𝑛(𝑥)+1 2 .</p>

<p> Indeed, the output function that we will use is the softmax which is: 𝑠𝑜𝑓𝑡𝑚𝑎𝑥(𝑥𝑖 ) = 𝑒 𝑥𝑖 ∑ 𝑒 𝑥𝑗 𝑗 , that enhances the proximity of the output to the one-hot. Finally, and as usual for the softmax, as a loss function we will use the categorical cross entropy: 𝑑(𝑦, 𝑦̂) = − ∑𝑖 𝑦𝑖 · 𝑙𝑜𝑔(𝑦̂𝑖 ).</p>

 <p> Before analyzing results we tested several configurations of hyperparameters of the network and we stayed with the best one. Then, we ploted the evolution of accuracy and we showed the confusion matrix to analyze the results.</p>
 
 <img alt="Result0" src="/assets/img/clasificador_bolas1.png" />
 <img alt="Result1" src="/assets/img/clasificador_bolas2.png" />
 
 ## Contributors
 <p><em>Alberto Melián Rodríguez</em></p>
 <p><em>Federico Colleluori</em></p>
