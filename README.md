# Landmark-classification-neural-net
Train a nueral net to classify images from a list of 10 cities based on landmarks

Objective: Given a picture, classify what is the city in the picture. 

Training Data: 30,000 images from Google Landmark Recognition Challenge for 10 specific cities. 

Method: Use a convolutional neural network (CNN) with a softmax activation output to predict the probability that a picture belongs to each of the 10 cities. This was implemented using Keras TensorFlow packages. I decided to use a CNN for this problem because the inputs were images and convulation layers can learn features of the images (edges, objects, etc.). For each convulation layer, there are multiple filters applied to the input images. Each filter has trainable parameters that learns features of the image. A 5x5 filter would have 25 parameters. CNN require little pre-processing of data before feeding it to the model. I resized all images to be the same dimensions (224, 224, 3). Since they are color images, each image had 3 layers for red, blue, and green colors. 

Instead of creating a neural net architecture from scratch and training all parameters, I decided to use a transfer learning approach and loaded pre-trained weights for the filters. I added additional fully connected layers at the end to learn my specific classification task for predicting probabilities for 10 cities. I used VGG-19 model which was pre-trained on the ImageNet dataset. This CNN has 19 layers; I kept the first 15 layers frozen (paramters are not adjusted) and set the last 4 layers to be trainable (updated based on my training data). I added 3 dense layers and a dropout layer on top of that, that took the flatten images from the CNN to learn the paramters to make the final predictions. 

Infrastructure: Due to the large amount of images and deep neural net, I setup an AWS EC2 instance with a GPU for faster processing power. Running the neural net on the GPU trains about 100x -1000x faster than uses my machine's CPU. 

Results:The accuracy on the unseen test data was 96.65%. The precision and recall values for each city were also calculated to see if there were patterns on misclassification. This is visualized in a confusion matrix. I found that the least accurately predicted city was Edinburgh, Scotland with a 91.3% true positive accuracy rate. This location is most confused Brugge, Belgium. 2.9% of pictures from Scotland are predicted as Belgium. This may be because these two countries are located near each other and may have similar acrchitecture and buildings which would make them difficult to tell apart. Also Scotland may not have a very distinct landmark that makes it easy to tell apart from other locations. 
