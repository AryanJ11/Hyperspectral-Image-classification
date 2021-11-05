# Hyperspectral Image classification
This project aims to employ state-of-the-art deep learning methods to perform Hyperspectral Image classification which would allow for an efficient and cost-effective method for applications such as remote sensing.

## Table of contents
* [Introduction](#introduction)
* [File Structure](#file-structure)
* [Model and Dataset](#model-and-dataset)
* [Results](#results)

## Introduction
Hyperspectral imaging is the method of capturing and processing of images across a large number of wavelengths or spectrum bands. Depending upon the technique used to perform this, the number of such bands can range between 100-200 or even more. One of the striking features of hyperspectral images is their application in remote sensing where they are used to distinguish earth surface features.

## File Structure
1. config: Includes details about the directories that are being used for accessing the dataset and checkpoints
2. Dataset_preparation: Includes all the methods used for preprocessing the data including train/test splits of the same.
3. models: Includes implementation of the entire model architecture.
4. train: Code for training the model including hyperparameters settings
5. Eval: Used for evaluating and selecting the best model based on the checkpoints saved during training.
6. pred: Used for performing predictions over the Hyperspectral Image.

## Model and Dataset
In this project I have used the Hierarchical Residual Network combined with Attention to successfully perform HSI classification. The model combines both the spatial and spectral features of the HSI by using different architectures for each of them, combining them and feeding them to Dense layer.

The _HresNet_ part of the architectures is same for both. It makes use of residuals or skip-connections which not only deals with the vanishing gradient problem but also enables extraction of multiscale features more flexibly which is essential for a classification task.

The input 3D image is first split into the desired number of scales(feature maps) which in this case has been set to 4. Mathematically speaking,

y_i=[
      x_i              i=1;
      K_i(x_i)         i=2;
      K_i(x_i+y_(i-1)) otherwise
    ]

where K_i(.) is a convolutional block for input x_i giving output y_i.

_Attention mechanism_ is used because different spatial pixels and spectral bands make unequal discriminative contributions to classification results.
Two different attention modules are used for spatial and spectral features as coded in models.ipynb file.

The _Dataset_ used for training the model is the Pavia Center Dataset which has a spatial size of 1096x715 and spectral size of 102 bands. There are 9 classes which are to be classified, which are shown in the Results section.

## Results
Following are the ground truth and predicted images along with the color coding of classes:

![Alt text](Images/org.png?raw=true "Title")

![Alt text](Images/tar.png?raw=true "Title")
