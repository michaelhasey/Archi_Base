
<img src="images/logo.png" width="50%" height="50%">
# Archi-Base


## About 

Archi_Vision is an AI tool that helps us learn more about urban housing and its relationship to the city.  Traditionally, housing data has been collected manually and contains few descriptors beyond house price, sqft, # of bathrooms,and so on.  As a result, housing remains largely undescribed and our understanding of its relationship to the city incomplete. Archi_Vision attempts to solve this by using Deep learning methods (object detection & classification) to rapidly extract far more detailed image-based housing data over larger areas than previously possible.

As proof of concept, I used Pittsburgh as a test area and trained my models on 750 hand-collected and labelled Google Street view images of working-class housing.  A a goal my project attempts to autonomously detect, analyze and record both standard visual housing data as well as new and novel info such as early signs of urban decline or gentrification including the presence or lack of abandoned buildings and the quality of sidewalks. Various concepts from class such as “Interpretability” and “Bias and Anonymity” were integrated.  


![](Images/houses.png)



## Table of Contents

- [GUI](#GUI)
- [Models](#Models)
- [Datasets](#Datasets)
- [References](#References)
- [Citation](#Citation)


## GUI

The proposed GUI provides further ai transparency through white-box methods such as prediction and data visualizations and simple explanations, required human input to correct model prediction mistakes or uncertainties therefore building trust in the model, both baseline and expert model adjustment capabilities, therefore staisfying the needs of users with varying ai or cs knowledge, and easy to understand prompts and suggestions regarding determining the appropriate model and settings to satisfy particular goals.

![](Images/gui.png)


## Models

### Summary:  
4 different models and corresponding notebooks were used for this experiment. 

### Model 1: Training for Vacant House Detection

```
python "Vacancy_Image_Classification_Training_Model.ipynb"
```

#### Model Overview

- A single label classification model used to train a convolutional neural network algorithm 
  to detect whether a house appears to be occupied or vacant.
- The model is built upon the fastai framework and pytorch (pyimage) computer vision library
- Model is trained on aprox. 200 hand selected images of working class houses from Pittsburgh that 
- have been manually sorted based on occupancy (occupied or vacant)
- This code was learned and adapted from various tutorials for and methods suggested by Fastai, an
online platfor that makes building, using and manipulating deep learning algorithms easier and
more accessible to cs and deep learning beginners.
- https://docs.fast.ai/tutorial.vision.html#Single-label-classification

#### Code modification and additions

- Though this tutorial was followed, various significant modifications and additions to thecode           
  were neccessary to achieve the goals of this project. they include: 
- setting up general framework of model and file structure
- modification of image transormation variables prior to training
- modification of batch size and image scale dependent on need and available computing power
- modification of learner rates after a series of experimentation with various learning rates
- learner rate of between le-4 and le-2 were found to be most suitable to achieve highest accuracy 
  and lowest loss function
- model results and confusion rates helped to provide further guidance to finely tune image 
  transformations, batch sizes and learning rate
  to achieve best results.

 
 
### Model 2: Detecting Vacant Houses

```
python "Vacancy_Image_Classification_Prediction_Model.ipynb"
```

![](Images/vacancy.png)

#### Model Overview

- A single label classification model that uses the weights obtained in training model (model 1) 
  to detect whether a house appears to be occupied or vacant.
- The model also labels and sorts images into folders with corresponding names.
- The model is built upon the fastai framework and pytorch (pyimage) computer vision library
- This code was learned and adapted from various tutorials for and methods suggested by Fastai, an
online platform that makes building, using and manipulating deep learning algorithms easier and
more accessible to cs and deep learning beginners.
- https://docs.fast.ai/tutorial.vision.html#Single-label-classification

#### Code modification and additions

- Though this tutorial was followed, various significant modifications and additions to thecode           
  were neccessary to achieve the goals of this project. they include: 
- setting up general framework of model and file structure
- loading and using custom trained weights from previous training model (model 1)
- custom labelling and sorting tool that provides corresponding file and folder labels 
  depending on predicted class.
- This allows easy identification of predicted class of all images after model has run
   
  
  
### Model 3: Detecting Building Features

```
python "Arch_Features_object_detection.ipynb"
```

<img align="left" src="Images/House_Detection2.gif">

<br clear="left"/>

### 

#### Model Overview

- This model uses Objectron 2, Facebook AI Research's next generation software system 
  that implements state-of-the-art object detection algorithms to detect and predict the type of
  architectural features (either door, window or general building volume) are present in images 
  and videos of working class houses in Pittsburgh.
- torchvision 1.7.0. used for computer vision library
- @misc{wu2019detectron2,
  author =       {Yuxin Wu and Alexander Kirillov and Francisco Massa and
                    Wan-Yen Lo and Ross Girshick},
    title =        {Detectron2},
    howpublished = {\url{https://github.com/facebookresearch/detectron2}},
    year =         {2019}
-  Model is trained on images that were manually collected from Google Street 
   View and labelled manually on sixGill, an online platform that simplifies AI
   deployment and contains rapid image dataset labelling tools
-  https://sixgill.com/
-  These trained images are located within the github repository within the data folder
- The included code was learned and adapted from various tutorials and sources including
   1. The official Detectron 2 Tutorial:
      https://colab.research.google.com/drive/16jcaJoc6bCFAQ96jDe2HwtXj7BMD_-m5
   2. Sage Elliot: my friend and research partner who has collaborated with me on a few 
      different AI deep learning projects.  He provided the bulk of the below code and a great deal 
      of guidance and advice when learning how to run, impliment and adapt the below 
      objectron 2 code for this project.

#### Code modification and additions

- Though much of the code was provided by the facebook tutorial and Sage, various significant 
  modifications  and additions to thecode were neccessary to achieve the goals of this project. 
  they include: 
- setting up general framework of model and file structure
- hand collecting aprox. 200 images from Google street view and labelling over aprox. 500 individual objects
  to be used for the training dataset.
- custom modifications to solver max iteration, model weight type appropriate for Coco detection 
  & faster rcnn convolutional model, batch size, number of object detection classes, and score
  threshold size when determining which prediction certainty rate (as shown in percentage) should 
  be used when making predictions and displaying results on image.
          
   
   
### Model 4: Detecting Sidewalk Cracks

```
python "Sidewalks_Detectron2_object_detection.ipynb"
```
<img align="left" src="Images/crack_detection.gif">

<br clear="left"/>

### 

#### Model Overview

- This model uses Objectron 2, Facebook AI Research's next generation software system 
  that implements state-of-the-art object detection algorithms to predict and classify sidwalk quality
  in images of residential streets around Pittsburgh.
- torchvision 1.7.0. used for computer vision library
- @misc{wu2019detectron2,
  author =       {Yuxin Wu and Alexander Kirillov and Francisco Massa and
                    Wan-Yen Lo and Ross Girshick},
    title =        {Detectron2},
    howpublished = {\url{https://github.com/facebookresearch/detectron2}},
    year =         {2019}
-  Model is trained on images that were manually collected from Google Street 
   View and labelled manually on sixGill, an online platform that simplifies AI
   deployment and contains rapid image dataset labelling tools
-  https://sixgill.com/
-  These trained images are located within the github repository within the data folder
- The included code was learned and adapted from various tutorials and sources including
   1. The official Detectron 2 Tutorial:
      https://colab.research.google.com/drive/16jcaJoc6bCFAQ96jDe2HwtXj7BMD_-m5
   2. Sage Elliot: my friend and research partner who has collaborated with me on a few 
      different AI deep learning projects.  He provided the bulk of the below code and a great deal 
      of guidance and advice when learning how to run, impliment and adapt the below 
      objectron 2 code for this project.

#### Code modification and additions

- Though much of the code was provided by the facebook tutorial and Sage, various significant 
  modifications  and additions to thecode were neccessary to achieve the goals of this project. 
  they include: 
- setting up general framework of model and file structure
- hand collecting aprox. 200 images from Google street view and labelling over aprox. 500 individual objects
  to be used for the training dataset.
- custom modifications to solver max iteration, model weight type appropriate for Coco detection 
  & faster rcnn convolutional model, batch size, number of object detection classes, and score
  threshold size when determining which prediction certainty rate (as shown in percentage) should 
  be used when making predictions and displaying results on image.
   




## Datasets

#### Training Dataset 1 - Vacant vs Occupied Housing Images
- 200 images in total (100 vacant, 100 occupied) of working class houses in Pittsburgh, PA.
- Hand collected from Google street view 
- manually labelled and sorted into corresponding folders 

#### Training Dataset 2 - Architectural Features
- 197 images of working class houses in Pittsburgh, PA.
- hand collected from Google street view 
- hand labelled on SixGill platform
        
#### Training Dataset 3 - Sidewalk Quality
- 104 images of various quality level sidewalks in Pittsburgh, PA.
- hand collected from Google street view
- hand labelled using image segmentation on SixGill platform
        
        
        * Data available upon request

## References

1. https://docs.fast.ai/tutorial.vision.html#Single-label-classification
2. https://github.com/facebookresearch/detectron2
3. www.sixgill.com
4. https://colab.research.google.com/drive/16jcaJoc6bCFAQ96jDe2HwtXj7BMD_-m5


## Citation

If you find our work and dataset useful in your research, please consider citing:

``` 
@misc{mhasey2021,
    title={Archi_Vision},
    author={Michael Hasey},
    year={2021},
}
```












## Description

Archi_base is a tool to automatically create very large datasets of labelled and sorted architectural imagery for ML / AI based modeling. It is meant to be used by architects, design offices, researchers, academics, students & anyone else who is interested in using architectural images to train deep neural networks.

The current method of aggregating large databases of architectural imagery are inadequate and slow.  Traditionally, if a user wants to acquire a dataset of thousands of images of a particular architects work, they need to manually search multiple image sources, filter through non-relevant images, download relevant images and then sort them into folders that correspond with their view (interior images, exterior images, aerial images, etc).  On average, it takes about 1 minute and 50 seconds to manually look for, download, and sort 10 images.  As a result, the manual method would take 30 hours of manual labour to build a robust dataset of 10,000 images for deep neural network training.  

Archi_Base solves this problem by providing a autonomous tool to rapidly search for, find, download, and sort images into their corresponding subject folders.  Instead of taking 30 hours to manually create a 10,000 image dataset, archi_base can complete this task in just over an hour with zero human interaction needed.

In order to do this, Archi_base employs a 3-step pipeline that leverages sofisticated AI & ML computer vision technology.  For the first step, Archi_base builds a ResNet-32 Image Classification model that is trained on a set of 2000 labelled images sorted into 5 different categories (aerial views, street views, close-up views, views of architectural textures, and interior views).  In step 2, the user is asked to identify the target, or the subject of the dataset.  This will be the topic that Archi_base searches and aggregates images for and can be anything from an architects name, an architectural firm, an architectural style or a particular building.  Then, the user is asked to specify the number of images to be included in the datset.  This can be anything from 100 images to well over 100,000 dependent on image availability.  After entering this information, Archi_base uses automatically employs a webscraper to find and download images associated with enetered target query and within the range amount specified.  In step 3, the final step, archi_base uses the previously created and trained ResNet-32 model to classify each downloaded image, label it and then place it into its corresponding folder.  For example, if an image is taken of a building from a street view location, Archi_Base will classify it as being in the "Street view" category, will label it as "streetview_1", and then place it into the "streetview" folder.  After step 1, 2 and 3 are complete, the result is a very large, labelled and robust dataset of sorted architectural imagery of the search query specified.

As this process only requires the user to specify the target subject and amount, Archi_base works in a completely autonomous fashion and saves the user a huge amount of time and effort.  While a robust 100,000 image dataset would take 330 hours to create manually, Archi_base completes this task in just 16 hours.

Currently, Archi_base is the fastest and easiest way to make custom, very large and robusy architectural imagery datasets for AI deep learning projects of any kind.
    
## Data
    
- 2000 images of architectural related subjects

    - zaha hadid building images
        - 300 street view images
        - 300 interio view images
        - 300 aerial view images
        - 300 close-up view images
        - 300 architectural texture images

    - miscellaneous images
        - 200 books / posters images
        - 100 people images
        - 200 drawings / sketches images

## Collab Notebooks

1. 1_Training_Model.ipynb

    - Resnet-32 (deep residual learning neural network for image recognition)
    - FastAi architecture & backend
    - PyTorch library
    
2. 2_Scraper_Predictor_Model.ipynb

    - instagram_scraper tool
    - FastAi architecture & backend
    - PyTorch library
    - Smash Mouth - "All Star" auto-complete song
    

## Slideshow Presentation

1. Archi_Base_Capstone_Hasey.pdf
