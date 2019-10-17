# face-recognition

I have used vgg face model as my base model
The structure of the VGG-Face model is demonstrated below.
![VGG-Face model](images/vgg-face-model.png)
Research paper denotes the layer structre as shown below.
![VGG-Face layers from original paper](https://i2.wp.com/sefiks.com/wp-content/uploads/2018/08/layer-details-in-vgg-face.png?w=1645&ssl=1)
link to the pre-trained model's weight is [here](https://drive.google.com/open?id=1CPSeum3HpopfomUEK1gybeuIVoeJT_Eo)

used transfer learning for the perpose of this assingment. 
trained the model by keeping the bottom layers unfrozen and other layers frozen  

compiled the model by using Adam optimizer with learning rate equal to 1e-5, 
categorical_crossentropy is used as the loss function and categorical_accuracy as the Evaluation Metric

categorical_accuracy checks to see if the index of the maximal true value is equal to the index of the maximal predicted value.  
Categorical crossentropy is a loss function that is used for single label categorization. This is when only one category is applicable for each data point. In other words, an example can belong to one class only.  
Use categorical crossentropy in classification problems where only one result can be correct.

## Note

This model is trained on Google Colabrotory with GPU enabled runtime.
after traning for arround 400 epochs I got the categorical_accuracy as 70-75%.
I have used Google Colabrotory just to train the custom VGG-Face model. and later downloaded that model to my local drive in order to recognise face from webcam.

# How to use

First install MTCNN. [MTCNN](https://arxiv.org/abs/1604.02878) is a deep learning arcitecture for facial detection.  
I have used `ImageDataGenerator` for traning the model. For traning I had to make a special directory scructure in order to use `ImageDataGenerator`. First there are two directy test and train, and each of them contain 6 sub directories, one for each class of our traning and sample. all the sub directories are named as there respective class ('Scarlett Johansson', 'Willa Holland', 'alexandra daddario', 'amber heard face', 'anne hathaway', 'kaushal'). Each sub directory contains only the face of the respective persons.  
Load the pretrainde VGG-Face model from [here](https://drive.google.com/open?id=1CPSeum3HpopfomUEK1gybeuIVoeJT_Eo). Pretrained model is in .h5 format. Load the model using `load_model()`   
Then remove the bottom layers of the VGG-Face model and add your coustom layers accourding to your need. I have added a dence layer, a dropout layer and a softmax layer   
Train the new custom model with `flow_from_directory`. I trained the model for around 400 epochs. Train the model upto your setisfaction.  
First I kept the layers of original VGG-Face model frozen and traind only the newly added layers.  
Then fine tuned the entire model.  
You can save the model using `save()`. Weights for custom model in [here](https://drive.google.com/open?id=1-986GG-7dzeTzLKqS7RpMkVUVoeFAt2I)  
Now you have MTCNN to detect the face and custom VGG-Face model to recognise the face.
Use OpenCV to read the image. Pass it to MTCNN to detect faces. Pass the detected Faces to our custom VGG_Face model to recognise it







