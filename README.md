# Airplane-Detection-using-R-CNN

### Object Detection ###

Object detection combines image classification and object localization tasks together. Object Localization is the process of locating one or more objects in an image with the help of a bounding box around it. The input to the object detection is an image and the output is one or more bounding boxes around the object along with the class label. The algorithm produces a list of object categories present in the image along with the axis-aligned bounding boxes indicating the position and scale of each instance of each object category.


### R-CNN ###

R-CNN refers to Region-Based Convolutional Neural Network. R-CNN model can be decomposed into three sub-modules. 

#### 1. Module : Region Proposal #### 
It generates and extracts category independent region proposals using Selective Search 

#### 2. Module : Feature Extractor ####
Extract features from each candidate region using a convolutional neural network

#### 3. Module : Classifier ####
Classify features as one of the classes known by using SVM classifier

![image](https://user-images.githubusercontent.com/55786239/142241153-93dd9973-1ea1-414c-bb6f-06e3652b4b93.png)


#### Region Proposals ####

Region proposals can be deemed as small parts of the original image, that we think might contain the object we are looking for. There are many different region proposal algorithms we can choose from. One widely used algorithm is selective search.

Selective search generates sub-segmentation in the first step and generates many candidate regions, In the next step, the greedy algorithm is used to combine recursively all similar regions to form larger regions. In the end, these generated regions are used to produce the final candidate region proposal. 
About 2000 candidate region proposals are given by selective search algorithm


#### Feature Extractor ####

The 2000 candidate region proposals are wrapped into a fixed size square and are fed as input to Convolutional Neural Network. The network process the region proposals and outputs a 4096-dimensional feature vector. In the paper, AlexNet is used as a feature extractor. But in this repository ResNet50 is used as a feature extractor. The input to ResNet50 should be of dimension (224,224,3). To fulfil the prerequisite all the candidate region proposals are wrapped to the input size of ResNet50.


#### Classifier ####

The final step is to classify the feature vectors of the CNN. We need to detect the class the object belongs to. SVM classifier is used for this task. One SVM is used for each object class and all of them are used. The output of SVM is the confidence score about how confident the particular feature vector represents the object class. 

The drawback of the network is the sub tasks cannot be done parallelly. So, in the end it takes lot of time to give the output.

### Data Info ###

The dataset is of total 733 images with number of airplanes varying each image. Annotation files for the corresponding image is saved in the .csv format. 

