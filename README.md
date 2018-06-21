# object-detection-model
Real time object detection using YOLO and Darknet

You only look once (YOLO) is a state-of-the-art, real-time object detection system. On a Pascal Titan X it processes images at 30 FPS and has a mAP of 57.9% on COCO test-dev.
YOLOv3 is extremely fast and accurate. In mAP measured at .5 IOU YOLOv3 is on par with Focal Loss but about 4x faster. Moreover, you can easily tradeoff between speed and accuracy simply by changing the size of the model, no retraining required!

Our model has several advantages over classifier-based systems. It looks at the whole image at test time so its predictions are informed by global context in the image. It also makes predictions with a single network evaluation unlike systems like R-CNN which require thousands for a single image. This makes it extremely fast, more than 1000x faster than R-CNN and 100x faster than Fast R-CNN.

Detection Using A Pre-Trained Model

This post will guide you through detecting objects with the YOLO system using a pre-trained model. If you don't already have Darknet installed, you should do that first. Or instead of reading all that just run:

git clone https://github.com/pjreddie/darknet
cd darknet
make
Easy!

You already have the config file for YOLO in the cfg/ subdirectory. You will have to download the pre-trained weight file here (237 MB). Or just run this:
wget https://pjreddie.com/media/files/yolov3.weights

1.
Then run the detector!
./darknet detect cfg/yolov3.cfg yolov3.weights data/dog.jpg

Darknet prints out the objects it detected, its confidence, and how long it took to find them. We didn't compile Darknet with OpenCV so it can't display the detections directly. Instead, it saves them in predictions.png. You can open it to see the detected objects. Since we are using Darknet on the CPU it takes around 6-12 seconds per image. If we use the GPU version it would be much faster.

I've included some example images to try in case you need inspiration. 
Any image or object which we want to detect must be placed inside 'Data' folder.Then run the detector.
Try data/eagle.jpg, data/dog.jpg, data/person.jpg, or data/horses.jpg!

The detect command is shorthand for a more general version of the command. It is equivalent to the command:


./darknet detector test cfg/coco.data cfg/yolov3.cfg yolov3.weights data/dog.jpg

Instead of supplying an image on the command line, you can leave it blank to try multiple images in a row. Instead you will see a prompt when the config and weights are done loading:

2.
./darknet detect cfg/yolov3.cfg yolov3.weights
then it ask for image path
Enter an image path like data/horses.jpg


3.
Changing The Detection Threshold
By default, YOLO only displays objects detected with a confidence of .25 or higher. You can change this by passing the -thresh <val> flag to the yolo command. For example, to display all detection you can set the threshold to 0:

./darknet detect cfg/yolov3.cfg yolov3.weights data/dog.jpg -thresh 0
Which produces:

So that's obviously not super useful but you can set it to different values to control what gets thresholded by the model.

Tiny YOLOv3
We have a very small model as well for constrained environments, yolov3-tiny. To use this model, first download the weights:

wget https://pjreddie.com/media/files/yolov3-tiny.weights
Then run the detector with the tiny config file and weights:

./darknet detect cfg/yolov3-tiny.cfg yolov3-tiny.weights data/dog.jpg
