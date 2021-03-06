# **Traffic Sign Recognition** 

## Writeup

### You can use this file as a template for your writeup if you want to submit it as a markdown file, but feel free to use some other method and submit a pdf if you prefer.

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

[image1]: ./examples/visualization.jpg "Visualization"
[image2]: ./examples/grayscale.jpg "Grayscaling"
[image3]: ./examples/random_noise.jpg "Random Noise"
[image4]: ./examples/placeholder.png "Traffic Sign 1"
[image5]: ./examples/placeholder.png "Traffic Sign 2"
[image6]: ./examples/placeholder.png "Traffic Sign 3"
[image7]: ./examples/placeholder.png "Traffic Sign 4"
[image8]: ./examples/placeholder.png "Traffic Sign 5"

## Rubric Points
### Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/481/view) individually and describe how I addressed each point in my implementation.  

---
### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one. You can submit your writeup as markdown or pdf. You can use this template as a guide for writing the report. The submission includes the project code.

You're reading it! and here is a link to my [project code](https://github.com/Ventu012/P3_TrafficSignClassifier/blob/main/Traffic_Sign_Classifier.ipynb)

### Data Set Summary & Exploration

#### 1. Provide a basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.

I used the pandas library to calculate summary statistics of the traffic signs data set:
* The size of training set is 34799
* The size of the validation set is 4410
* The size of test set is 12630
* The shape of a traffic sign image is (32, 32, 3)
* The number of unique classes/labels in the data set is 43

#### 2. Include an exploratory visualization of the dataset.

Here is an exploratory visualization of the data set.  
In the images below we can see one example of traggic sign for every output class.

<div align="center">
    <img src="https://github.com/Ventu012/P3_TrafficSignClassifier/blob/main/report_images/one_image_per_class.png" width="500" />
</div>
  
In the image below we can see the number of images per class of the Training Dataset.  

<div align="center">
    <img src="https://github.com/Ventu012/P3_TrafficSignClassifier/blob/main/report_images/Number_of_Images_per_Class.png" width="500" />
</div>


### Design and Test a Model Architecture

#### 1. Describe how you preprocessed the image data. What techniques were chosen and why did you choose these techniques? Consider including images showing the output of each preprocessing technique. Pre-processing refers to techniques such as converting to grayscale, normalization, etc. (OPTIONAL: As described in the "Stand Out Suggestions" part of the rubric, if you generated additional data for training, describe why you decided to generate additional data, how you generated the data, and provide example images of the additional data. Then describe the characteristics of the augmented training set like number of images in the set, number of images for each class, etc.)

As a first step, I decided to not convert the images to grayscale but leave them in RGB.  
As a secondo step, I decided to normalize the image data, its better to convert image data with zero mean and equal variance. Images come in 0 to 255 pixle value, the normalization step is done by applying the formula: (image_data - X_Mean) / X_Mean, and output -1 to 1 pixel value.

#### 2. Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

My final model consisted of the following layers:

| Layer 				|     Description 								| 
|:---------------------:|:---------------------------------------------:| 
| Input 				| 32x32x3 RGB image   							| 
| Convolution 5x5   	| 1x1 stride, same padding, Outputs = 28x28x6 	|
| RELU					|												|
| Max pooling			| 2x2 stride,  Outputs = 14x14x6 				|
| Convolution 5x5   	| 1x1 stride, same padding, Outputs = 10x10x16 	|
| RELU					|												|
| Max pooling			| 2x2 stride,  Outputs = 5x5x16 				|
| Flatten   			| Outputs = 400  								|
| Fully connected		| Outputs = 120  								|
| Dropout   			| Keep probability – 0.75   					|
| Fully connected		| Outputs = 84  								|
| Dropout   			| Keep probability – 0.75   					|
| Fully connected		| Outputs = 43  								|
|						|												|
 


#### 3. Describe how you trained your model. The discussion can include the type of optimizer, the batch size, number of epochs and any hyperparameters such as learning rate.

To train the model I decided to use a batch size of 128 and a number of epochs equals to 70.  
Also I decided to use ADAM Optimizer since it gives better accuracy than SGD optimizer.  

#### 4. Describe the approach taken for finding a solution and getting the validation set accuracy to be at least 0.93. Include in the discussion the results on the training, validation and test sets and where in the code these were calculated. Your approach may have been an iterative process, in which case, outline the steps you took to get to the final solution and why you chose those steps. Perhaps your solution involved an already well known implementation or architecture. In this case, discuss why you think the architecture is suitable for the current problem.

My final model results were:
* training set accuracy of 0.996
* validation set accuracy of 0.947
* test set accuracy of 0.929

If a well known architecture was chosen:
* What architecture was chosen?  
    I chose to use the LeNet-5 architecture used also in the lesson and the following parameters:
    * Learning Rate = 0.001
    * Epoch = 70
    * Batch Size = 128

* Why did you believe it would be relevant to the traffic sign application?  
    We use the same architecture in the lessons to clossify traffic signs so I decided to use the same architecture improving the paramers to obtain better results.

* How does the final model's accuracy on the training, validation and test set provide evidence that the model is working well?  
    Bolow the Training and Validation accuracy during training
    
    <div align="center">
        <img src="https://github.com/Ventu012/P3_TrafficSignClassifier/blob/main/report_images/accuracy_train_validation.png" width="500" />
    </div>
 

### Test a Model on New Images

#### 1. Choose five German traffic signs found on the web and provide them in the report. For each image, discuss what quality or qualities might be difficult to classify.

Here are ten German traffic signs that I found on the web:

<div align="center">
    <img src="https://github.com/Ventu012/P3_TrafficSignClassifier/blob/main/report_images/test_images.png" width="500" />
</div>

#### 2. Discuss the model's predictions on these new traffic signs and compare the results to predicting on the test set. At a minimum, discuss what the predictions were, the accuracy on these new predictions, and compare the accuracy to the accuracy on the test set (OPTIONAL: Discuss the results in more detail as described in the "Stand Out Suggestions" part of the rubric).

Here are the results of the prediction:

|					Image						|					Prediction 					| 
|:---------------------------------------------:|:---------------------------------------------:| 
| Right-of-way at the next intersection  		| Right-of-way at the next intersection  		|
| Priority road 								| Priority road 								|
| Stop 											| Stop 											|
| No entry  									| No entry  									|
| General caution  								| General caution  								|
| Bumpy road  									| Road narrows on the right 					|
| Slippery road  								| Slippery road  								|
| Road work  									| Road work  									|
| Traffic signals   							| Slippery road  								|
| Go straight or left  							| Go straight or left  							|

The model was able to correctly guess 8 of the 10 traffic signs, which gives an accuracy of 80%.  
In detail it fails to predict the Bumpy road and the Traffic signals.  

#### 3. Describe how certain the model is when predicting on each of the five new images by looking at the softmax probabilities for each prediction. Provide the top 5 softmax probabilities for each image along with the sign type of each probability. (OPTIONAL: as described in the "Stand Out Suggestions" part of the rubric, visualizations can also be provided such as bar charts)

The code for making predictions on my final model is located in the 25th cell of the Ipython notebook.  

For the first image, the model is relatively sure that this is a 'Right-of-way at the next intersection' sign (probability of 1), and the image does contain a 'Right-of-way at the next intersection' sign. 

The top five soft max probabilities for each image were
<div align="center">
    <img src="https://github.com/Ventu012/P3_TrafficSignClassifier/blob/main/report_images/top_softmax_probabilities.png" width="500" />
</div>

For each image the probability of the correct prediction was:

| Probability 			|					Prediction 					| 
|:---------------------:|:---------------------------------------------:| 
| 100% 					| Right-of-way at the next intersection  		|
| 100% 					| Priority road 								|
| 100% 					| Stop 											|
| 100% 					| No entry  									|
| 100% 					| General caution  								|
| 2% 					| Bumpy road  									|
| 100% 					| Slippery road  								|
| 100% 					| Road work  									|
| 0% 					| Traffic signals  								|
| 100% 					| Go straight or left  							|


### (Optional) Visualizing the Neural Network (See Step 4 of the Ipython notebook for more details)
#### 1. Discuss the visual output of your trained network's feature maps. What characteristics did the neural network use to make classifications?

* Featuremap for the first Convolutional layer which is having output shape of 28x28x6
<div align="center">
    <img src="https://github.com/Ventu012/P3_TrafficSignClassifier/blob/main/report_images/conv_layer_1_image.png" width="500" />
</div>

* Featuremap for the first Max Pool layer which is having output shape of 14x14x6
<div align="center">
    <img src="https://github.com/Ventu012/P3_TrafficSignClassifier/blob/main/report_images/max_pool_layer_1_image.png" width="500" />
</div>

* Featuremap for the second Convolutional layer which is having output shape of 10x10x16
<div align="center">
    <img src="https://github.com/Ventu012/P3_TrafficSignClassifier/blob/main/report_images/conv_layer_2_image.png" width="500" />
</div>

* Featuremap for the first Max Pool layer which is having output shape of 5x5x16
<div align="center">
    <img src="https://github.com/Ventu012/P3_TrafficSignClassifier/blob/main/report_images/max_pool_layer_2_image.png" width="500" />
</div>
