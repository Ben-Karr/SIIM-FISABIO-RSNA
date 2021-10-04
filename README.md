# SIIM-FISABIO-RSNA

Build  a pipeline, from Data Preparation to Prediction, for the [SIIM-FISABIO-RSNA](https://www.kaggle.com/c/siim-covid19-detection) kaggle competition. The goal is to classifie images of chest radiographs and to predict bounding boxes of areas of interest (i.e. aiding medical staff in identifying COVID19 infections).

### 1. [Prepare the Dataframe](https://github.com/Ben-Karr/SIIM-FISABIO-RSNA/blob/master/01_Prepare%20Dataframe.ipynb)
Join the two source dataframes and prepare the bounding boxes and labels for training.

### 2. [Resize the Bounding Boxes](https://github.com/Ben-Karr/SIIM-FISABIO-RSNA/blob/master/02_Resize%20boxes.ipynb)
Resize the bounding boxes to fit the (resized) images of width 1024. The images will have the same aspect ratio as the original, so if h_n is the new height, w_o, h_o the old width and height then:
1024/h_n = w_o/h_o and there is a scalar α such that (1024, h_n) = α (w_o, h_o). Save that scalar to the dataframe.

### 3.1 [Resize the train Images](https://github.com/Ben-Karr/SIIM-FISABIO-RSNA/blob/master/03_Resize%20images.ipynb)
Use the scalar from the previous step to resize the images to a width of 1024. This step is done to use `.png` files instead of the `.dicom` of the dataset and to have an uniform image width, aswell as to reduce computation time.

### 3.2 [Resize the test Images](https://github.com/Ben-Karr/SIIM-FISABIO-RSNA/blob/master/03_Resize%20images%20TEST.ipynb)
Get the scalar as in step 2 and resize the test images as in step 3.1.

### 4. [Build a Classifier](https://github.com/Ben-Karr/SIIM-FISABIO-RSNA/blob/master/04_Learn_Classifier.ipynb)
Use a XResNet50 architecture to predict one of four labels for each image.

### 5. [Build a Bounding Box Regressor](https://github.com/Ben-Karr/SIIM-FISABIO-RSNA/blob/master/05_Learn_bbox.ipynb)
Use a RetinaNet with the XResNet50 encoder from step 4. to predict a list of bounding boxes for each image. The implementation for the RetinaNet is from [asvcode](https://github.com/asvcode/fmi) and a lot of the utility functions are from the [Bounding Box notebook](https://github.com/fastai/course-v3/blob/master/nbs/dl2/pascal.ipynb) of the fastai coursev3 Part 2.

___Note:___  Step 4 and 5 are set up in such a way that you can switch back and forth between the two by sharing the XResNet encoder. Thus both learners can "focus on their task" but also profit from the other.

### 6. [Predict Labels & Bounding boxes for the test set](https://github.com/Ben-Karr/SIIM-FISABIO-RSNA/blob/master/06_Predict.ipynb)
Get the resulting learners from step 4 and 5 and predict on the test set - both on a study level (using the classifier to predict labels) as well as on an image level (using the Regressor to predict Bounding Boxes). Undo the scaling of the images (in the preprocessing step 3.2 & in the learner step 4) and bring the predictions in the competition format.