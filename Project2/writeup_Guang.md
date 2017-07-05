#**Traffic Sign Recognition** 

##Writeup for Traffic Sign Classification Project

---

**Build a Traffic Sign Recognition Project**

The goals / steps of this project are the following:
* Load the data set (see below for links to the project data set)
* Explore, summarize and visualize the data set
* Design, train and test a model architecture
* Use the model to make predictions on new images
* Analyze the softmax probabilities of the new images
* Summarize the results with a written report


[//]: # (Image References)

[image1]: ./examples/original_data_distribution.jpg "Distribution"
[image2]: ./examples/15samples.jpg "Original pictures"
[image3]: ./examples/grayscale.jpg "Grayscaling"
[image4]: ./examples/normalized_grayscale.jpg "Normalized Grayscale"
[image5]: ./examples/augmentation.jpg "Data Augmentation"
[image6]: ./examples/Augmented_data_distribution.jpg "Augmentation Distribution"
[image7]: ./examples/test_validation_accuracy.jpg "Accuracy History"
[image8]: ./examples/my_sign.jpg "My Traffic Sign"
[image9]: ./examples/prediction.jpg "Traffic Sign Prediction"

## Rubric Points
###Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/481/view) individually and describe how I addressed each point in my implementation.  

---
###Writeup / README

####1. Provide a Writeup / README that includes all the rubric points and how you addressed each one. You can submit your writeup as markdown or pdf. You can use this template as a guide for writing the report. The submission includes the project code.

You're reading it! and here is a link to my [project code](https://github.com/dongguang82/Udacity_car_term1/blob/master/Project2/Traffic_Sign_Classifier_Guang0702_v4.ipynb)

###Data Set Summary & Exploration

####1. Provide a basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.

I used the numpy library to calculate summary statistics of the traffic
signs data set:

* The size of training set is 34799
* The size of the validation set is 4410
* The size of test set is 12630
* The shape of a traffic sign image is 32x32x3(3 chanels)
* The number of unique classes/labels in the data set is 43

####2. Include an exploratory visualization of the dataset.

Here is an exploratory visualization of the data set. It is a bar chart showing how the data dustributed. We can see that the training data set is not equally distributed, some categories gave much more data than others, such like class #1 and class #2.

![alt text][image1]

###Design and Test a Model Architecture

####1. Describe how you preprocessed the image data. What techniques were chosen and why did you choose these techniques? Consider including images showing the output of each preprocessing technique. Pre-processing refers to techniques such as converting to grayscale, normalization, etc. (OPTIONAL: As described in the "Stand Out Suggestions" part of the rubric, if you generated additional data for training, describe why you decided to generate additional data, how you generated the data, and provide example images of the additional data. Then describe the characteristics of the augmented training set like number of images in the set, number of images for each class, etc.)

As a first step, I decided to convert the images to grayscale because some reserchers shew they achieved very high accuracy, and also converting the pictures to grayscale make the data size smaller since the chanel number is reduced from 3 to 1.

Here are 15 examples of traffic sign image before grayscaling.

![alt text][image2]

Here are 15 examples of traffic sign image after grayscaling.

![alt text][image3]

As the last step, I normalized the image data because it can lead to better convergence usually. Here is how it looks like after the normalization operation using a simple equation (pixel - 128)/ 128.

![alt text][image4]

Then, I decided to generate additional data because the training data is not uniformly distributed, some categories have more data than others.

To add more data to the the data set, I used the image transformation techniques such as cv2.warpAffine and cv2.warpPerspective.

Here is a random example of an original image and the augmented images:

![alt text][image5]

After the data augmentation, I merged the training data and the vlidation data then regenerate the validation data, which is 20% of the total data except the test data. The function of train_test_split is used from the sklearn module. From the distribution of the augmented data, we can see there are at least 1500 data in all the categories in the training data.

![alt text][image6]

####2. Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

My final model consisted of the following layers:

| Layer         		|     Description	        					|
|:---------------------:|:---------------------------------------------:|
| Input         		| 32x32x1 grayscale image   							|
| Convolution 5x5     	| 2x2 stride, valid padding, outputs 28x28x6 	|
| RELU					|												|
| Max pooling	      	| 2x2 stride,  outputs 14x14x6 				|
| Convolution 5x5	    | 2x2 stride, valid padding, outputs 10x10x16    |
| RELU					|												|
| Max pooling	      	| 2x2 stride,  outputs 5x5x16 				|
| Flatten				|												|
| Fully connected		| input 400, output 120        									|
| RELU					|												|
| Dropout				| 50% keep        									|
| Fully connected		| input 120, output 84        									|
| RELU					|												|
| Dropout				| 50% keep        									|
| Fully connected		| input 84, output 43        									|


####3. Describe how you trained your model. The discussion can include the type of optimizer, the batch size, number of epochs and any hyperparameters such as learning rate.

To train the model, I used the defult LeNet with two layer of convolution layers and three layer of fully connected layers.  I used the AdamOptimizer with a learning rate of 0.0009.  The epochs used was 50 while the batch size was 128.  Other important parameters I learned were important was the number and distribution of additional data generated.  I played around with various different distributions of image class counts and it had a dramatic effect on the training set accuracy.  It didn't really have much of an effect on the test set accuracy, or real world image accuracy.  Finally, I was able to get 95.1% accuracy with virtually no changes on the test set. Here is the convergence plot for the training set and validation set.

![alt text][image7]

####4. Describe the approach taken for finding a solution and getting the validation set accuracy to be at least 0.93. Include in the discussion the results on the training, validation and test sets and where in the code these were calculated. Your approach may have been an iterative process, in which case, outline the steps you took to get to the final solution and why you chose those steps. Perhaps your solution involved an already well known implementation or architecture. In this case, discuss why you think the architecture is suitable for the current problem.

My final model results were:
* training set accuracy of 0.997
* validation set accuracy of 0.992 
* test set accuracy of 0.951
 

###Test a Model on New Images

####1. Choose five German traffic signs found on the web and provide them in the report. For each image, discuss what quality or qualities might be difficult to classify.

Here are five German traffic signs that I found on the web:

![alt text][image8] 


####2. Discuss the model's predictions on these new traffic signs and compare the results to predicting on the test set. At a minimum, discuss what the predictions were, the accuracy on these new predictions, and compare the accuracy to the accuracy on the test set (OPTIONAL: Discuss the results in more detail as described in the "Stand Out Suggestions" part of the rubric).

Here are the results of the prediction:

| Image			        |     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| 60 km/h	      		| 60 km/h						 				|
| Ahead Only			| Ahead Only      							|
| Bumpy Road			| Bumpy Road     							|
| General Caution    			| General Caution  										|
| Stop Sign      		| Stop sign   									| 
| Yield					| Yield											|


The model was able to correctly guess 4 of the 5 traffic signs, which gives an accuracy of 80%. 

####3. Describe how certain the model is when predicting on each of the five new images by looking at the softmax probabilities for each prediction. Provide the top 5 softmax probabilities for each image along with the sign type of each probability. (OPTIONAL: as described in the "Stand Out Suggestions" part of the rubric, visualizations can also be provided such as bar charts)

The code for making predictions on my final model is located in the 11th cell of the Ipython notebook.

For the first image, the model is relatively sure that this is a stop sign (probability of 0.6), and the image does contain a stop sign. The top five soft max probabilities were

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| 0.467 | 60 km/h						 				|
| 1.0			| Ahead Only      							|
| 1.0			| Bumpy Road     							|
| 1.0	  | General Caution  										|
| 1.0	  | Stop sign   									| 
| 1.0			| Yield											|

![alt text][image9] 

### (Optional) Visualizing the Neural Network (See Step 4 of the Ipython notebook for more details)
####1. Discuss the visual output of your trained network's feature maps. What characteristics did the neural network use to make classifications?


