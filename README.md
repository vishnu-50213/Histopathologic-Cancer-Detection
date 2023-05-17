# Histopathologic-Cancer-Detection
Introduction
This notebook provides solution to Histopathologic Cancer Detection challenge on Kaggle. This is a perfect Computer Vision problem where we are tasked with the detection of cancer by identifying metastatic tissue in histopathologic scans of lymph nodes using Deep Learning.

Header Image

1. Understanding the Problem:

Our goal is to create an algorithm to identify metastatic cancer in small image patches taken from larger digital pathology scans.

Obviously I don't know biology to understand this problem right away, here is what I found online about histopathology.

Histopathology is the study of the signs of the disease using the microscopic examination of a biopsy or surgical specimen that is processed and fixed onto glass slides. To visualize different components of the tissue under a microscope, the sections are dyed with one or more stains.
Motivation:

Lymph nodes are small glands that filter the fluid in the lymphatic system and they are the first place a breast cancer is likely to spread. Histological assessment of lymph node metastases is part of determining the stage of breast cancer in TNM classification which is a globally recognized standard for classifying the extent of spread of cancer.

The diagnostic procedure for pathologists is tedious and time-consuming as a large area of tissue has to be examined and small metastases can be easily missed.
That makes using Machine Learning a great choice both in terms of accuracy and ease of usability. It could bring a great change altogether.

2. Understanding the Data:

The train data we have here contains 220,025 images and the test set contains 57,468 images.

It is important to take into account that this data is only a subset of the original PCam dataset which in the end is derived from the Camelyon16 Challenge dataset, which contains 400 H&E stained whole slide images of sentinel lymph node sections that were acquired and digitized at 2 different centers using a 40x objective. The PCam's dataset including this one uses 10x undersampling to increase the field of view, which gives the resultant pixel resolution of 2.43 microns.

Here's what Kaggle says,

The original PCam dataset contains duplicate images due to its probabilistic sampling, however, the version presented on Kaggle does not contain duplicates. We have otherwise maintained the same data and splits as the PCam benchmark.
Our training data has a class distribution of 60:40 negative and positive samples which is not bad.

I also found that these data were obtained as a result of routine clinical practices and similar to how a trained pathologist would examine similar images for identifying metastases. However, some relevant information about the surroundings might be left out with these small-sized image samples (I guess).

3. Understanding the Images

You are predicting the labels for the images in the test folder. A positive label indicates that the center 32x32px region of a patch contains at least one pixel of tumor tissue. Tumor tissue in the outer region of the patch does not influence the label. This outer region is provided to enable fully-convolutional models that do not use zero-padding, to ensure consistent behavior when applied to a whole-slide image.
This from the competition's description means that the centers of the images are the ones that really matter.

As you might already know, this is a binary classification problem.

4. Understanding the Evaluation Metric

The evaluation metric is the Area Under ROC Curve which is also called AU-ROC/AOC Curve. It is one of the most important evaluation metrics for checking any classification model’s performance.

AUC - ROC curve is a performance measurement for classification problem at various thresholds settings. ROC is a probability curve and AUC represents degree or measure of separability. It tells how much model is capable of distinguishing between classes. Higher the AUC, better the model is at predicting 0s as 0s and 1s as 1s. By analogy, higher the AUC (close to 1), better the model is at distinguishing between patients with disease and no disease. The curve is plotted with True Positive Rates Vs the False Positive Rates along the x and y axes respectively.
