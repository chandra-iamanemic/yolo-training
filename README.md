# yolo-training

This is a small guide to training custom objects using the yolo object detection algorithm.

## Clone repo

Download or clone the darknet repository : (darknet repo)[https://github.com/pjreddie/darknet]

The data used for training is a collection of images with the desired object to be trained. 
Each of these images have to accompanied by a text file containing the coordinates of the bounding box and the name 
of the text file should be the same as that of the image. (1.jpg and 1.txt = this is one sample)

## Setup to train the network

  *The training data must be placed inside darkent/data/obj 
  *Each of the training sample image's path relative to darknet folder must be listed in a text file called train.txt
  *For making train.txt, use the prep_yolo_train.py from this repo. (Place the images in a folder called images and run the code)
  *Create a file named obj.names containing the labels of image classes (in our example its closed and open)
  *Create a file obj.data that points the paths of all the files required for begining the training process(Example in repo)
  
  This is how your obj.data file must look like (ignore the comments in the brackets) :
  classes = 2
  train = /home/csi/Documents/Chandra/yolo/darknet/data/train.txt (path to train.txt)
  valid = /home/csi/Documents/Chandra/yolo/darknet/data/test.txt  (path to test.txt (not necessary))
  names = /home/csi/Documents/Chandra/yolo/darknet/data/obj.names (path to obj.names file)
  backup = weights/hands  (relative location inside darknet folder where the weights are saved during training process)
  
  
  
  *The model uses a starting point of weights which are trained on imagenet and we must feed this weights file to start training
    (Link to Pre-Trained Weigts)[https://pjreddie.com/media/files/darknet53.conv.74]
  *A cfg file is used which contains the network information such as the architecture, number of layers, number of filters used etc.
  *We make slight modifications to the cfg file and edit the filters according to the number of classes we have.
  *In our example we have two classes (number of classes + 5)*3 = 21, Where ever the filters = 21 in the cfg file in repo, you can replace those with the number of filters according to your classes.
  *The number of classes in the cfg file must also be changed accordingly.
  
## Training of the network

open your terminal and change into the darknet directory.

./darknet (path to obj.data) (path to cfg file) (path to the pre-trained weights)

example : 
./darknet detector train /home/csi/Documents/Chandra/yolo/darknet/data/obj.data /home/csi/Documents/Chandra/yolo/darknet/data/yolov3-hands.cfg /home/csi/Documents/Chandra/yolo/darknet/darknet53.conv.74

## Using the trained model
check out this repo : ()[https://github.com/chandra-iamanemic/yolo_object_detection]
