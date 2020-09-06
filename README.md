# Image-Steganalysis

## Overview
[Steganography](https://hal-utt.archives-ouvertes.fr/hal-02542075/document) is usually referred to as the techniques and methods that allow to hide information within an innocuous-like cover object. The resulting stego-object resembles, as much as possible, the original cover object. Therefore it can be sent over an unsecured communication channel that may be subject to wiretapping by an eavesdropper.

This project was made for the [ALASKA2 Image Steganalysis competition on Kaggle](https://www.kaggle.com/c/alaska2-image-steganalysis).



## Purpose
[Data](https://www.kaggle.com/c/alaska2-image-steganalysis/data) can be hidden within images using 3 main algorithms - JMiPOD, JUNIWARD, UERD.
The average message length is 0.4 bit per non-zero AC DCT coefficient.
The images are all compressed with one of the three following JPEG quality factors: 95, 90 or 75.

The purpose of this project was to build an efficient algorithm that detects secret data hidden within innocuous-like digital images.
More specifically, for a given image, our algorithm outputted a positive number if it predicted hidden data and a negative number if it predicted no hidden data.

## Key points about our method

1. We applied transfer learning on efficientnet-b0. 
    We tried other networks such as resnet-50. But after initial tests, we found that efficientnet-b0 gave the best results.
    We believe that efficientnet-b4 would give even better results. However, we didn't have the GPU power necessary to train this bigger model.

2. We used multi-class classification instead of binary classification.
    While training, we set cross-entropy loss to the classification of the individual algorithms JMiPOD, JUNIWARD, UERD.
    We tried binary classification too. Multi-class classfication seemed to work better.
    
3. We applied simple image flips and transforms for data-augmentation.

## Scoring

We evaluated our submissions on a [weighted AUC](https://www.kaggle.com/c/alaska2-image-steganalysis/overview/evaluation)

tpr_thresholds = \[0.0, 0.4, 1.0]
weights = \[2, 1]

We were happy to achieve a score of 0.797.


## To use

[Format your data](https://www.kaggle.com/c/alaska2-image-steganalysis/data).  
Load the effnet weights in effnetmodelv2.pth into the effnet-b0 model. \
Run the test function on the effnet model.
