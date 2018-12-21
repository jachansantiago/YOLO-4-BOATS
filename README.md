# YOLO-4-BOATS

Manuel Alvarez,
Jeffrey Chan,
Anthony Ortiz,		
Jose Quiñones,

## Outline:
The following code is a real-time object detection algorithm based on the programm You Only Look Once (YOLO), by Joseph Redmon, Ali Farhadi. More specifically, we used YOLOv2 and Tiny YOLOv3. The data used was extracted from Pascal VOC 2

## What's YOLO?:
YOLO is a program of real-time object detection that, as its name suggest, runs the convolutional neural network (CNN) and classifiers only once per sample. This trait makes YOLO much faster than competitors. Is also important to mention that YOLO threats object detection as a regression problem. YOLOv2 have 19 convolutional layers and 5 maxpooling layers, while tiny-YOLOv3 only has 13 convolutional layers.

## Structure of Data:
The image used were extrated from PASCAL VOC data sets. We were able to get 508 images and their labels. Unfortunately, the labels were not already orginize as YOLO require. But fortunately, YOLO had a script for PASCAL VOC labels managing, as to organize them correctly. It, therefore, arrenge the labels text to have [Class, x, y, width, height], where x, y represent the coordinates of the center of the boundary box.

## Output:
The output of the programm are the image given with the predicted boundary. This constituted a problem to the metric since we are not given the error values such as accuracy or precision.

## How to run:

![Diagram to train markdown](https://drive.google.com/uc?id=1hI5UkgwMV6Nw-SB1E4dnfAy8Hj5kcqNI)

### Download darknet.
```{bash}
git clone https://github.com/pjreddie/darknet
cd darknet
make
```

### Download the dataset:

```{bash}
wget http://pjreddie.com/media/files/VOCtrainval_11-May-2012.tar
wget http://pjreddie.com/media/files/VOCtest_06-Nov-2007.tar
tar -xvf VOCtrainval_11-May-2012.tar
tar -xvf VOCtest_06-Nov-2007.tar
```

### Download the pre-trained weights:

```{bash}
wget https://pjreddie.com/media/files/darknet53.conv.74
```

### Proccess the metdata to feed it into darknet.

```{bash}
python voc_label.py
python test_voc_label.py
```

### To train YOLO

#### Train YoloV2
```{bash}
./darknet/darknet detector train boats.data cfg/yolov2-boats.cfg darknet53.conv.74
```

#### Train Yolo Tiny V3
```{bash}
./darknet/darknet detector train boats.data cfg/yolov3-tiny-boats.cfg darknet53.conv.74
```

### Predict using our pre-trained networks:

#### YoloV2
 
Dowload weights [Here](https://drive.google.com/file/d/1pOVeu-YjcqSRafPvYQHAZoiQMdNV_9OZ/view?usp=sharing)

```{bash}
./darknet/darknet detector test boats.data cfg/yolov2-boats.cfg weights/yolov2.backup < test.txt
```

#### Yolo Tiny V3

```{bash}
./darknet/darknet detector test boats.data cfg/yolov3-tiny-boats.cfg weights/yolov3-tiny-boats_30000.weights < test.txt
```
