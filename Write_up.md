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
- steps: 2500
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
- steps: 2500
- learning rate: consine decay learning rate
- Data augmentation: 
  - Brigthness
  - Contrast
  - Saturation
  - Hue
  - Black Patches
  
  
#### Image example
![alt text](./images/data_augmentation_bis.PNG "example of augmented image") 

#### Graphs
As the learning remained unchanged, the learning rate won't be displayed here.

![alt text](./images/Exp_one_loss.PNG "Losses chart of the experience n°1") 

First the overall loss has significantly decreased compare to the initial experiment which proves that the data augmentation is effective and improving the object detection. The regularization loss has also the same shape than the reference. Another improvement is the stagnation of the classification loss which here seems to constantly decrease over the training. Which makes me think over increasing the number of steps or increase the learning rate. The same situation happen on the localisation loss.

The regularization loss show us that we still don't have any overfit with our model.

#### Conclusion 

Augmenting the volume and variety of data has greatly improve the training of our model by reducing the loss. Therefore it is still possible to improve the performances of the model. Two leads are the number of steps and the learning rate.

### Learning Rate Fine Tunning
As state in the following article the cosine decay rate is already a great learning rate for the object detection [Article](https://neptune.ai/blog/tensorflow-object-detection-api-best-practices-to-training-evaluation-deployment). So Instead of providing a new learning rate, the experiment will be with the same learning rate but with a different set of parameters.

**Initial experiment:**
```
 learning_rate {
        cosine_decay_learning_rate {
          learning_rate_base: 0.04
          total_steps: 2500
          warmup_learning_rate: 0.013333
          warmup_steps: 200
        }
```

**Experiment on learning rate:**
```
 learning_rate {
        cosine_decay_learning_rate {
          learning_rate_base: 0.05
          total_steps: 2500
          warmup_learning_rate: 0.01
          warmup_steps: 300
        }
```

The training was perform with the folowing parameter:

- optimizer: momentum optimizer
- steps: 2500
- learning rate: Fine tuned consine decay learning rate
- Data augmentation: 
  - Brigthness
  - Contrast
  - Saturation
  - Hue
  - Black Patches
#### Graphs
![alt text](./images/Exp_two_loss.PNG "Losses chart of the experience n°2") 

Incsreasing the learning rate caused a shift from one minimum to another and caused the weights to shift to a sub-optimal minimum.

![alt text](./images/Exp_two_learning_rate.PNG "Learning rates chart of the experience n°2") 

This simply display the learning rates.

#### Conclusion

The higher learning rate made the model to skip from a minimum to another one and this minimum seemed to be sub-optimal. The next interation will focus on increasing the number of steps.

### Increase Steps Number experiment
The previous experiment and documentation showed that the learning rate was already close to an optimum and then following one of our previous experiment conclusion we will here increse the number of steps by 500.

The training was perform with the folowing parameter:

- optimizer: momentum optimizer
- steps: 3000
- learning rate: Fine tuned consine decay learning rate
- Data augmentation: 
  - Brigthness
  - Contrast
  - Saturation
  - Hue
  - Black Patches

# Conclusion