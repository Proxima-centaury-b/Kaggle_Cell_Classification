## Table of contents
* [The Problem](#the-problem)
* [The Dataset](#the-dataset)
* [Tech Stack](#tech-stack)



This was the final project of my Data Science bootcamp at Jedha. I had chance to work with two highly motivated tech-women on this topic.
The main problem was to find a way to identify precise patterns in human protein cell images. From a data scientist point of view, this was a multi-label classification model (18 labels) with Image Segmentation.

## The Problem
Given human cells images with different regions of interest (called [organelles](https://en.wikipedia.org/wiki/Organelle)),
predict the protein organelle localization labels for **each cell** in the image. In other terms, we have to predict the **type** and **localization** of these [organelles](https://en.wikipedia.org/wiki/Organelle) given a random image consisting of many (often different) human cells. 


![RGB](https://github.com/Proxima-centaury-b/Kaggle_Cell_Classification/blob/main/RGB.png)   ///////////////////////////////////////////![mask](https://github.com/Proxima-centaury-b/Kaggle_Cell_Classification/blob/main/mask.png)

                
The left image is the combination of three "channel" images (Red Green Blue) into a single colorfull image where we can see different cells. The right image is a **multilabel mask**
 obtained by Image Segmentation, which allows to localize each cells in the image. However, the problem is to localize each protein of interest inside each cells in the image.


At first sight, this problem seemed to be quite standard to handle, I mean using techniques of image classification model. But there were several complex considerations we have to deal with : 
- Volume = the size of dataset : huge for computations (running-time problems), but not enough for acceptable training accuracy (need Data Augmentation and other tricks)
- Variety of images: comprises 17 different cell types of highly different morphology, which affect the protein patterns of the different organelles.
- Velocity : recurrent problems of huge running-times due to size of dataset and training with Deep Neural Networks (200+ layers)
- Highly multi-labelled : there are in total 19 different labels present in the dataset (18 labels for specific locations, and label 18 for negative and unspecific signal)


Moreover, the labels we have to predict are **weak** image-level labels which means that the labels for training are **image level labels** while the task is to predict **cell level** labels which is totally different, and much more complicated. That is to say, each training image contains a number of cells that have collectively been labeled and the prediction task is to look at images of the same type and predict the labels of each individual cell within those images.

As the training labels are a collective label for all the cells in an image, it means that each labeled pattern can be seen in the image but not necessarily that each cell within the image expresses the pattern. This imprecise labeling is what is refer to as **weak**.


## The Dataset

Train and test sets were provided by The Human Protein Atlas research group  which is an initiative based in Sweden that is aimed at mapping proteins in all human cells, tissues, and organs regrouping leading researchers all around the world. These dataset was quite huge and consisted of :

- 21.186 images of high resolution 
- a total of 160GB storage

So this was a real Big Data problem, which required many tricks to avoid endless computation, as we had to put our images (by batches) in a very deep Neural Network consisting 200+ layers and 4+ millions training parameters (derived from the so-called EfficientNetB0). For this task, we used GPU hardware provided by Kaggle to reach acceptable running-times (up to 12-15 hours)


## Tech Stack

#Python #Tensorflow #Deep Learning #Computer Vision #Transfert Learning 

> A thorough description of the problem is available on Kaggle's website : https://www.kaggle.com/c/hpa-single-cell-image-classification/overview/description 



