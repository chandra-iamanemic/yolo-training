# yolo-training

This is a small guide to training custom objects using the yolo object detection algorithm.

## Clone repo

Download or clone the darknet repository : [darknet repo](https://github.com/pjreddie/darknet)

The data used for training is a collection of images with the desired object to be trained. 
Each of these images have to accompanied by a text file containing the coordinates of the bounding box and the name 
of the text file should be the same as that of the image. (1.jpg and 1.txt = this is one sample)

## The label file (text file)
The text file accompanying the image should contain these 5 values :
1. class number
2. x-centre of the bounding box/width of total image (absolute value of x-centre)
3. y-centre of the bounding box/heigth of total image (absolute value of y-centre)
4. (width of the bounding box/width of total image)
5. (height of the bounding box/height of total image)

As it can be seen, we take the relative or absolute values of the coordinates (w.r.t total image coordinates)
Hence we have the 4 values in the range (0 to 1)

example of txt file :
0 0.3 0.24 0.6 0.4

## Setup to train the network

  * The training data must be placed inside darkent/data/obj 
  * Each of the training sample image's path relative to darknet folder must be listed in a text file called train.txt
  * For making train.txt, use the prep_yolo_train.py from this repo. (Place the images in a folder called images and run the code)
  * Create a file named obj.names containing the labels of image classes (in our example its closed and open)
  * Create a file obj.data that points the paths of all the files required for begining the training process(Example in repo)
  
  This is how your obj.data file must look like (ignore the comments in the brackets) :
  1. classes = 2
  2. train = /home/csi/Documents/Chandra/yolo/darknet/data/train.txt (path to train.txt)
  3. valid = /home/csi/Documents/Chandra/yolo/darknet/data/test.txt  (path to test.txt (not necessary))
  4. names = /home/csi/Documents/Chandra/yolo/darknet/data/obj.names (path to obj.names file)
  5. backup = weights/hands  (relative location inside darknet folder where the weights are saved during training process)
  
  
  
  * The model uses a starting point of weights which are trained on imagenet and we must feed this weights file to start training
    [Link to Pre-Trained Weigts](https://pjreddie.com/media/files/darknet53.conv.74)
  * A cfg file is used which contains the network information such as the architecture, number of layers, number of filters used etc.
  * We make slight modifications to the cfg file and edit the filters according to the number of classes we have.
  * In our example we have two classes (number of classes + 5)*3 = 21, Where ever the filters = 21 in the cfg file in repo, you can replace those with the number of filters according to your classes.
  * The number of classes in the cfg file must also be changed accordingly.
  
## Training of the network

open your terminal and change into the darknet directory.

./darknet detector train (path to obj.data) (path to cfg file) (path to the pre-trained weights)

example : 
./darknet detector train /home/csi/Documents/Chandra/yolo/darknet/data/obj.data /home/csi/Documents/Chandra/yolo/darknet/data/yolov3-hands.cfg /home/csi/Documents/Chandra/yolo/darknet/darknet53.conv.74

## Testing on a single image 
./darknet detector test (path to obj.data) (path to cfg file) (path to your trained weights) (path to the test image)

## Using the trained model
check out this repo : https://github.com/chandra-iamanemic/yolo_object_detection
