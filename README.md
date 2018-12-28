# Introduction
Latest advancement in AI technology and deep learning algorithms are changing the retail industry. With large number of
data sets comprising thousands of shelf images, companies can now leverage of AI to better monitor their retail shelf
presence. AI will help in recognizing product conditions on shelf such as availability, assortments, space, pricing,
promotions and many more. It will empower companies to take immediate corrective. AI algorithms provide accurate stock
visibility insights. In this project we present algorithms to detect and count the retail objects using Open CV and Deep
Learning techniques. The first step is to detect the objects and draw boundaries around them. The second step is to count
the boundaries to get a total count of the objects in the image.

## Methodology

We have adopted various images recognition techniques to achieve the retail object counting.
1. Tradition Open CV Techniques
  - Thresholding
  - Edge Detection
  - Background Removal
  - Contour Detection
2. Deep Learning Techniques
  - Faster RCNN
  - Multi-box Single Shot Detector (SSD)
  
  
## 1. Tradition Open CV Techniques
### Binary Otsu Thresholding

The first step in our approach was to binarize the image to differentiate the foreground and background. Since the normal
thresholding requires a hardcoded set of threshold values we adopted Otsu thresholding for thresholding to dynamically
binarize the images. 

### Edge Detection

The next step was the do the edge detection. We used canny edge detection, this requires hardcoding the minimum and
maximum threshold values. We used a dynamic method the identify the threshold values. The algorithm we used to identify
the minimum and maximum threshold values is by identifying the median of the histogram of pixel intensity. The histogram
should be equalized. Then the minimum and maximum threshold values are calculated using
Min threshold – 0.66*median
Max threshold – 1.33*median
 
### Background Removal

The background was removed using floodfill technique. The following are the steps followed in floodfill technique.
1. Read in the image.
2. Threshold the input image to obtain a binary image.
3. Flood fill from pixel (0, 0). The background is filled with white now.
4. Invert the flood filled image in step 3.
5. Combine the thresholded image with the inverted flood filled image using bitwise OR operation to obtain the final
foreground mask with holes filled in.

### Contour Detection

The final step is to find contours on the flood filled images. During contour detection there are lot of noisy contours. We
implemented an algorithm to remove the unwanted contours. The following are the steps in identifying the correct contours.
1. Identify the external contours using findcontours.
2. Sort the contours in the descending order of the contour area.
3. Start from the first contour and iterate through the contours. If the contour area is less than 80% of the previous
contour area limit the contours to that point.
4. Create a convex hull of all the relevant contours

### Detecting objects via OpenCV
![Images which OpenCV detected well](https://raw.githubusercontent.com/siddhantmaharana/counting-objects/master/opencv.jpg)


### Problematic detection with OpenCV
![Images where OpenCV failed](https://raw.githubusercontent.com/siddhantmaharana/counting-objects/master/opencv_problems.jpg)


## 2. Deep Learning Techniques

### TensorFlow Object Detection API with SSD model with Mobilenet

TensorFlow Object Detection API can be used with different pre-trained models. In this project, a SSD model with
Mobilenet (ssd_mobilenet_v1_coco) was chosen. The model had been trained using MSCOCO Dataset which consists of
2.5 million labeled instances in 328 000 images, containing 91 object types such as “person”, “cat” or “dog”. The
ssd_mobilenet_v1_coco-model is reported to have mean Average Precision (mAP) of 21 on COCO dataset. In this project,
the SSD model was tested both as pre-trained without fine tuning and as fine-tuned.

### TensorFlow Object Detection API with Faster RCNN model

Faster RCNN models have a superior performance compared to the SSD models and it was tried out as well. For the project,
a faster RCNN model trained on MSCOCO data set was used.
Similar to above, a threshold of 15 percent was used to count the objects in the dataset.
The Faster RCNN trained on Open Images by google on was fed to the Object Detection API and tested on the dataset with
similar thresholds for detecting bounding boxes and categories.

### Detecting objects with RCNN
![Images which RCNN detected](https://raw.githubusercontent.com/siddhantmaharana/counting-objects/master/rcnn.jpg)
![Images which RCNN detected](https://raw.githubusercontent.com/siddhantmaharana/counting-objects/master/rcnn_2.jpg)



