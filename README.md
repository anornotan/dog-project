[//]: # (Image References)

[image1]: ./images/sample_dog_output.png "Sample Output"
[image2]: ./images/vgg16_model.png "VGG-16 Model Keras Layers"
[image3]: ./images/vgg16_model_draw.png "VGG16 Model Figure"
## Project Overview

In this project I implemented a CNN with AWS GPU to, given an image of either a dog or a human, classify the most resembling dog breed among 118 available breeds. I used two pre-trained models `ResNet-50` to detect dogs and `OpenCV-CascadeClassifier` to detect humans. 

![Sample Output][image1]

Steps I took to run the Jupyter notebook on GPU on AWS:
- Create an EC2 instance in which I selected the `Ubuntu x64 with Tensorflow` as my AMI by following this [tutorial](https://hackernoon.com/keras-with-gpu-on-amazon-ec2-a-step-by-step-instruction-4f90364e49ac).
- Use scp to transfer files to my instance
```sh
## cd to the folder containing privateKey.pem and the folder I want to upload 
## 
scp -i privateKey.pem -r folderToUpload  ubuntu@Public_DNS_(IPv4)
## replace ubuntu with ec2-user for Windows/OS
``` 
- To run Jupyter Notebook, first ssh to the instance. You can find more details in these [videos](https://www.youtube.com/watch?v=XJnpl7mQBIw).
```sh
ssh -i privateKey.pem ubuntu@Public_DNS(IPv4)

git clone https://github.com/udacity/dog-project.git

## download the dog dataset
wget https://s3-us-west-1.amazonaws.com/udacity-aind/dog-project/dogImages.zip

## download the human dataset
wget https://s3-us-west-1.amazonaws.com/udacity-aind/dog-project/lfw.zip

## download the VGG-16 bottleneck features
wget https://s3-us-west-1.amazonaws.com/udacity-aind/dog-project/DogVGG16Data.npz
```
- Then,
```sh
jupyter notebook --ip=0.0.0.0 --no-browser
### replace localhost with IPv4 Public IP in browser
```



## Suggestions to Make your Project Stand Out!

(Presented in no particular order ...)

#### (1) Augment the Training Data 

[Augmenting the training and/or validation set](https://blog.keras.io/building-powerful-image-classification-models-using-very-little-data.html) might help improve model performance. 

#### (2) Turn your Algorithm into a Web App

Turn your code into a web app using [Flask](http://flask.pocoo.org/) or [web.py](http://webpy.org/docs/0.3/tutorial)!  

#### (3) Overlay Dog Ears on Detected Human Heads

Overlay a Snapchat-like filter with dog ears on detected human heads.  You can determine where to place the ears through the use of the OpenCV face detector, which returns a bounding box for the face.  If you would also like to overlay a dog nose filter, some nice tutorials for facial keypoints detection exist [here](https://www.kaggle.com/c/facial-keypoints-detection/details/deep-learning-tutorial).

#### (4) Add Functionality for Dog Mutts

Currently, if a dog appears 51% German Shephard and 49% poodle, only the German Shephard breed is returned.  The algorithm is currently guaranteed to fail for every mixed breed dog.  Of course, if a dog is predicted as 99.5% Labrador, it is still worthwhile to round this to 100% and return a single breed; so, you will have to find a nice balance.  

#### (5) Experiment with Multiple Dog/Human Detectors

Perform a systematic evaluation of various methods for detecting humans and dogs in images.  Provide improved methodology for the `face_detector` and `dog_detector` functions.
