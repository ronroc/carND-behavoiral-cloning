## **Behavioral Cloning Project**

The goals / steps of this project are the following:

* Use the simulator to collect data of good driving behavior
* Build, a convolution neural network in Keras that predicts steering angles from images
* Train and validate the model with a training and validation set
* Test that the model successfully drives around track one without leaving the road
* Summarize the results with a written report


[//]: # (Image References)

[image2]: ./examples/first.jpg "Grayscaling"
[image3]: ./examples/second.jpg "Recovery Image"
[image4]: ./examples/third.jpg "Recovery Image"

### Rubric Points
#### Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/432/view) individually and describe how I addressed each point in my implementation.  

---

### Files Submitted & Code Quality

#### 1. Submission includes all required files and can be used to run the simulator in autonomous mode

My project includes the following files:
* model.py containing the script to create and train the model
* drive.py for driving the car in autonomous mode
* model.h5 containing a trained convolution neural network
* writeup_report.md summarizing the results
* utils.py containing helper functions

#### 2. Submission includes functional code
Using the Udacity provided simulator and my drive.py file, the car can be driven autonomously around the track by executing
```sh
 python drive.py model.h5
```

#### 3. Submission code is usable and readable

The model.py file contains the code for training and saving the convolution neural network. The file shows the pipeline I used for training and validating the model, and it contains comments to explain how the code works.

### Model Architecture and Training Strategy

#### 1. An appropriate model architecture has been employed

My model consists of a convolution neural network with 5x5 and 3x3 filters  (model.py lines 22-57)

The model includes ELU layers to introduce nonlinearity and also takes care of the vanishing gradient problem , and the data is normalized in the model using a Keras lambda layer (code line 43). Dropout id used to take care of over fitting.

#### 2. Attempts to reduce overfitting in the model

The model contains dropout layers in order to reduce over fitting (model.py lines 49).

The model was trained and validated on different data sets to ensure that the model was not over fitting . The model was tested by running it through the simulator and ensuring that the vehicle could stay on the track.

#### 3. Model parameter tuning

The model used an Adam optimizer, so the learning rate was not tuned manually (model.py line 66).

#### 4. Appropriate training data

I used the sample training data shared in the course. Whatever training data I tried to generate wasn't accurate to be used in modelling

### Model Architecture and Training Strategy

#### 1. Solution Design Approach

Initially I generated the training data by diving around the track and saving the output .

 My first step was to use a convolution neural network model similar to the Architecture which was used by NVIDIA

In order to gauge how well the model was working, I split my image and steering angle data into a training and validation set.

I found that my first model had a low mean squared error on the training set but a high mean squared error on the validation set.

This implied that the model was overfitting.

To combat the overfitting, I modified the model by increasing the dropout. Then I tried increased the number of epochs

But the model  was not of much use as it  deviated from the track on a number of occasions.

Then I used the sample training dataset provided in the course  and followed a similar approach as detailed above

At the end of the process, the vehicle is able to drive autonomously around the track without leaving the road.

#### 2. Final Model Architecture

The final model architecture (model.py lines 18-24) consisted of a convolution neural network with the following layers and layer sizes

* Convolution: 5x5, filter: 24, strides: 2x2, activation: ELU
* Convolution: 5x5, filter: 36, strides: 2x2, activation: ELU
* Convolution: 5x5, filter: 48, strides: 2x2, activation: ELU
* Convolution: 3x3, filter: 64, strides: 1x1, activation: ELU
* Convolution: 3x3, filter: 64, strides: 1x1, activation: ELU
* Drop out (0.5)
* Fully connected: neurons: 100, activation: ELU
* Fully connected: neurons: 50, activation: ELU
* Fully connected: neurons: 10, activation: ELU
* Fully connected: neurons: 1 (output)

#### 3. Creation of the Training Set & Training Process

To capture good driving behavior, I first recorded two laps on track one using center lane driving. Here is an example image of center lane driving:

![alt text][image2]

I then recorded the vehicle recovering from the left side and right sides of the road back to center These images show what a recovery looks like starting from ... :

![alt text][image3]
![alt text][image4]

Since the training data which I generated did not help in training a robust model, sample dataset given in the course was used

After the collection process, I had 8037 number of left, center and right camera images and the steering angle which was used as inputs

Preprocessing of the data did not help to improve the accuracy. Methods used / tried can be found in utils.py

I finally randomly shuffled the data set and put 0.2% of the data into a validation set.

I used this training data for training the model. The validation set helped determine if the model was over or under fitting. The ideal number of epochs was 10 which was obtained after a few iterations. I used an adam optimizer so that manually training the learning rate wasn't necessary.

Disclosure - Methods in utils.py are forked from Siraj Raval github repo https://github.com/llSourcell
