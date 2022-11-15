# :robot: Neural Face Editor (NFE) :art:

Andrey Palaev, a.palaev@innopolis.university <br/>
Mikhail Rudakov, m.rudakov@innopolis.university <br/>
Anna Startseva, a.startseva@innopolis.university

## Table of Contents
- [Description](#description)
- [Project Architecture](#project-architecture)
- [Current Results](#current-results)
- [References](#references)

## Description
NFE is a tool that allows anyone to edit their anime pictures using Deep Learning to change attributes such as hair colour, hair length, eye colour etc.

The project is mainly inspired by works on interpreting the latent space of GANs for people face generation [1] and other methods of manipulating GAN output [2]. 
It leverages techniques mentioned in the papers to edit real users’ photos, change multiple image features, and preserve the general image content. 
These features for editing would probably include hair colour, eye colour, etc., which are not explored in the previous works.

## Project Architecture
![Step 1 and 2](images/image_generation_annotation.jpg)
![Step 3](images/svm.jpg)
Mainly adopted from Shen et al. [1], our project architecture consists of several models.

Stage 1 is image generation. StyleGAN is used to produce images of anime faces.

Stage 2 is generated image annotation. We use [illustration2Vec](https://github.com/rezoo/illustration2vec) proposed by Saito and Matsui [2] to tag images with tags we need.

Stage 3 is image classification. For the each attribute we want to be able to control further, we train a SVM for separating latent codes based on some feature. This would let us know the vector in which this feature changes in the latent space.

## Current Results
Sample generated images, produced by GAN: <br/>
![img.png](images/img.png)
Current results are far from perfect, but we will try to fix it in the future. Possible solutions are to try different, bigger dataset or to change model architecture.

As we stated before, we generated and labelled 10K samples. The dataset statistics is the following (the rest of values is NaN):
- Hair length <br/>
  ![Untitled](images/img1.png)
- Hair colour <br/>
  ![Untitled](images/img2.png)
- Eye colour <br/>
  ![Untitled](images/img3.png)
  
As we can see, there are a lot of NaN values. This is because the results are far from realistic ones and tagging tool is not 100% accurate (as it is a neural network)

In the future work , we may consider adding other attributes such as “Smile” and “Blush” or even “Quality” (to fix the artifacts) made by GAN.

## References
[1] Shen, Y., Gu, J., Tang, X., & Zhou, B. (2019). Interpreting the Latent Space of GANs for Semantic Face Editing. arXiv. https://doi.org/10.48550/arXiv.1907.10786 <br/>
[2] Upchurch, P., Gardner, J., Pleiss, G., Pless, R., Snavely, N., Bala, K., & Weinberger, K. (2016). Deep Feature Interpolation for Image Content Changes. arXiv. https://arxiv.org/abs/1611.05507v2
