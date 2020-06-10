# Archi_Base

## Description

Archi_base is a tool to automatically create very large datasets of labelled and sorted architectural imagery for ML / AI based modeling. It is meant to be used by architects, design offices, researchers, academics, students & anyone else who is interested in using architectural images to train deep neural networks.

The current method to aggregate large databases of architectural imagery is inadequate and slow.  In order to create a database of architectural imagery, a user is required to manually search multiple image sources, filter through non-relevant images, download relevant images then sort into folders that correspond.  On average, it about 1 minute and 50 seconds to look for, download, and sort 10 images.  As a result, it would take 30 hours of manual labour to build a robust dataset of 10,000 images for deep neural network training.  

Archi_Base solves this problem by probiding a tool to rapidly and autonomously search for, find, download, and sort images into their corresponding subject folders.  Instead of taking 30 hours to manually create a 10,000 image dataset, archi_base completes this task in just over an hour with zero human interaction needed.

In order to do this, Archi_base employs a 3-step pipeline that leverages sofisticated AI & ML computer vision technology.  Within step 1, Archi_base builds a ResNet-32 Image Classification model that is trained on a set of 2000 labelled images sorted into 5 different categories (aerial views, street views, close-up views, views of architectural textures, and interior views).  In step 2, the user is asked to identify the target search query.  This will be the topic that Archi_base searches and downloads images for.  It can be anything from an architects name, an architectural firm, an architectural style or a particular building.  In addition, the user is asked to specify the number of images to search.  After entering this information, Archi_base uses a webscraper to find and download images associated with enetered target query and within the range amount specified.  In step 3, archi_base uses the previously trained ResNet-32 model to classify each downloaded image and then label and place them into their corresponding folder.  For example, if an image is taken of a building from a street view location, Archi_Base will classify it as being in the "Street view" category then will label it as "streetview_1" and place it into the "streetview" folder.  After step 1, 2 and 3 are complete, the user will end up with a robust dataset of sorted architectural images that correspond with the search query specified.  

As this process only requires the user to specify the target subject and amount, Archi_base works in a completely autonomous fashion and saves the user a huge amount of time and effort.  While a robust 100,000 image dataset would take 330 hours to create manually, Archi_base can complet this task in 16 hours.

Currently, Archi_base is the fastest and easiest way to make custom, very large and robusy architectural imagery datasets for AI deep learning projects of any kind.


## Included Notebooks

1. 1_Training_Model.ipynb

    - Resnet-32 (deep residual learning neural network for image recognition)
    - FastAi architecture & backend
    - PyTorch library
    
2. 2_Scraper_Predictor_Model.ipynb

    - instagram_scraper tool
    - FastAi architecture & backend
    - PyTorch library
    - Smash Mouth - "All Star" auto-complete song
    
3. Data
    
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
