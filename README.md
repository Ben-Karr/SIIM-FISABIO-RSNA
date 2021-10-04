# SIIM-FISABIO-RSNA

Build  a pipeline, from Data Preparation to Prediction, for the [SIIM-FISABIO-RSNA](https://www.kaggle.com/c/siim-covid19-detection) kaggle competition. The goal is to classifie images of chest radiographs and to predict bounding boxes of areas of interest (i.e. aiding medical staff in identifying COVID19 infections).

### 1. [Prepare the Dataframe](https://github.com/Ben-Karr/SIIM-FISABIO-RSNA/blob/master/01_Prepare%20Dataframe.ipynb)
Join the two source dataframes and prepare the bounding boxes and labels for training.

### 2. [Build module to process dicom files](https://github.com/Ben-Karr/SIIM-FISABIO-RSNA/blob/master/02_Dicom%20Prep.ipynb)
Create functionality that removes extreme values, cuts black or white frames around the image, fixes and normalizes the dicom images

### 3. [Prepare images](https://github.com/Ben-Karr/SIIM-FISABIO-RSNA/blob/master/03_Prepare%20Data.ipynb)
Apply above functionality to dicom files, resize the images and save metadata to dataframe.

### 5. [Build Classifiers](https://github.com/Ben-Karr/SIIM-FISABIO-RSNA/blob/master/05_Learn_Classifier_timm.ipynb)
Build a simple EffNet Classifier with the timm library (https://github.com/rwightman/pytorch-image-models/blob/master/timm/models/efficientnet.py)

### 6. [Build a Bounding Box Regressor](https://github.com/Ben-Karr/SIIM-FISABIO-RSNA/blob/master/05_Learn_bbox.ipynb)
Use the icevision library (https://github.com/airctic/icevision) with fastai to try out different object detection models.
