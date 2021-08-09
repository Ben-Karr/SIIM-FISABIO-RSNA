# SIIM-FISABIO-RSNA

Build  a pipelin, from Data Preparation to Prediction, for the [SIIM-FISABIO-RSNA](https://www.kaggle.com/c/siim-covid19-detection) kaggle competition. The goal is to classifie images of chest radiographs and to predict bounding boxes of areas of interest (i.e. aiding medical staff in identifying COVID19 infections).

### 1. [Prepare the Dataframe](./01_Prepare\ Dataframe.ipynb)
Join the two source dataframes and prepare the bounding boxes and labels for training.

### 2. [Resize the Bounding Boxes](./02_Resize\ boxes.ipynb)
Resize the bounding boxes to fit the (resized) images of width 1024. The images will have the same aspect ratio as the original, so if $h_n$ is the new height, $w_o,h_o$ the old width and height then:
$\frac{1024}{h_n} = \frac{w_o}{h_o}$ and there is a scalar $α$ such that $(1024, h_n) = α \cdot (w_o,h_o)$. Save that scalar in the dataframe.

### 3.1 [Resize the train Images](./03_Resize\ images.ipynb)
Use the scalar from the previous step to resize the images to a width of 1024. This step is done to use `.png` files instead of the `.dicom` of the dataset and to have an uniform image width, aswell as to reduce computation time.

### 3.2 [Resize the test Images](04_Resize\ images\ Test.ipynb)
Get the scalar as in step 2 and resize the test images as in step 3.1.

### 4. []