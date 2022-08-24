# Project overview
This project is showing a variety of method to train a neural network over a given dataset. The neural network is train for object detection.
The objection detection module of a self driving vehicle is such an important module. This module help the vehicle to be aware of its surrounding. 
This way a vehicle can detect obstacle to avoid.

# Set up
To execute this training the provided workspace was used. 
All the different steps to execute this project can be found inside the file README.md

# Dataset
## Dataset analysis
This section should contain a quantitative and qualitative description of the dataset. It should include images, charts and other visualizations.

TODO: add pictures 

The dataset is composed by 1000 images from the waymo dataset. 
The first noticable fact is the vehicle/bicycle/pedestrian distribution their is a lot of cars and trucks but only a few bycicles and pedestrians.
Also most of the trips where done with daylight conditions and good weather conditions.

## Cross validation
For this project due to the smal amount of data (only 1000 images), the training data split will contain 80% of the images (800) and the validation data split will be composed by 20% (198). This is the Train-Test split strategy. The data is splitted randomly between the two sets. A few images will be used for test purpose between the 100 downloaded files 3 are disposed inside the test directory.
The split are considered before data augmentation.

# Training
## Reference experiment
As a reference experiment, the training was perform with the folowing parameter:

- optimizer: momentum optimizer
- learning rate: consine decay learning rate
- Data augmentation: Null

### Loss analysis

![alt text](./images/Init_exp_loss.png "Loss data of the Reference experiment") 

Analysis:

- the classification and localization losses don't seem to improve a lot across the training
- the regularization loss peak and then decrease to finaly stabelize.
- the validation curve doesn't show any overfit 
- the slow evolution of the regularization loss could come from the lack of data or the learning rate 

### learning

![alt text](./images/Init_exp_learning_rate.png "Learning of the Reference experiment") 

### Conclusion
This experiment 
The next experiments will focus on data augmentation and learning rate.

## Improve on the reference
### Data Augmentation
As the data set is quite small and fail to reflect some real life situation, data augmentation is used to improve the size and variety of the data set.

The training was perform with the folowing parameter:

- optimizer: momentum optimizer
- learning rate: consine decay learning rate
- Data augmentation: 
  - Brigthness
  - Contrast
  - Saturation
  - Hue
  - Black Patches
  
  
#### Image example
TODO: Add example of data augmentation

#### Graphs

TODO: Add Data Augmentation loss

### Learning Rate

