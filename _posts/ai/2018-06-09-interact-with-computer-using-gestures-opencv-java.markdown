---
layout: post
logo: "🎒"
title:  "Interact with computer using gestures: OpenCV & Java"
date:   2018-06-09
categories: Artificial Intelligence
permalink: /ai/interact-with-computer-using-gestures-opencv-java
description: Vision | Artificial Intelligence | Image Processing | Gesture Recognition
---

![JARVIS — Pretty cool, right?](https://miro.medium.com/max/1000/1*BxNsGcvZC8IUO33VIYAnNg.jpeg)
*JARVIS — Pretty cool, right?*

> Setup: [Using OpenCV Java with Eclipse and JavaCV](https://docs.opencv.org/master/d1/d0a/tutorial_java_eclipse.html)

In our daily life, we talk, we listen, we point, we see, and we use many other ways to interact with people and environment around us. However, when interacting with computers using just mouse and keyboard, we are quite limited regarding speed and convenience. So, why not use vision and speech.

In this article, I’ll be covering simple gestures and movement tracking using OpenCV to interact with computers.

## Capture Webcam Stream

You won’t be needing any fancy hardware to achieve this, just laptop’s inbuilt webcam or any external webcam is enough. We will start by capturing the webcam’s video stream and then apply image processing filters on each frame to identify gestures and track movements. For ease, I have used Red, Green and Blue colored props and their movement is acting as our input.

```
CvCapture capture = cvCreateCameraCapture(0);
IplImage image = cvRetrieveFrame(capture);
cvFlip(image, image, 1);
```

## Separating Color Channels

Each image is a 4D matrix of n x m dimension each, where n and m is width and height of image respectively. Each matrix represents rgba values of each pixel in the image and we will extract each of this values into individual 1D matrix.

```
IplImage red = IplImage.create(image.cvSize(), image.depth(), 1);
cvSplit(image, red, green, blue, null);
```

## Extracting Colors

We will need a grayscale image to subract it from color channel images to get image containing intensity of each color. Grayscale images carries only intensity information.

```
IplImage gray = IplImage.create(image.cvSize(), image.depth(), 1);
cvCvtColor(image,gray,CV_RGB2GRAY);

CvMat diff_red_mat = IplImage.create(image.cvSize(), image.depth(), 1).asCvMat();
cvSub(gray ,red , diff_red_mat, null);
```

What we have now is an image with only red color with high intensity as white and low intensity as black. We then apply Gaussian blur and Medium filter to remove unwanted distortions and small patches of the area with a low intensity of red values. Then we use binary threshold filter to fill the image with 0s for no red and 1s with for red.

```
cvSmooth(diff_red_mat, diff_red_mat, CV_MEDIAN, 75);
cvSmooth(bin_red, bin_red, CV_GAUSSIAN, 5);

IplImage bin_red = cvCreateImage(image.cvSize(), image.depth(), 1);
cvThreshold(diff_red_mat, bin_red, 20, 200, CV_THRESH_BINARY);
```

Learn more about [filters](https://docs.opencv.org/3.1.0/d4/d13/tutorial_py_filtering.html) and [thresholds](https://docs.opencv.org/2.4.13.4/doc/tutorials/imgproc/threshold/threshold.html).

## Finding Contours and Bounds

Contours are outline borders. Now we draw rectangles containing our contours bounding the object identified and use the center of the rectangle to track the movement of our props.

<script src="https://gist.github.com/div5yesh/63102903406bc6c27afb56e98b46c874.js"></script>

## Robot Class

Let the magic begin. A Robot class of Java AWT library which provides methods for generating inputs to move the mouse cursor, click and scroll. We will use rectangle bounds of single color prop to move our cursor and collision of any two rectangle bounds of two color props to perform a click, sort of like a pinch. We can also perform drag and drop using this gesture.

<script src="https://gist.github.com/div5yesh/8bf3f66e713d4f5c9180c3f0f4a2690c.js"></script>

Here `cursor` and `thumb` are bound rects of two different colored props.

# Endless Possibilities

With OpenCV and Robot class we can create endless use cases to interact with our computer using gestures. We can create a gesture recognizer to launch applications based on a combination of recorded gestures instead of just tracking the movement of props. This is just a simple example, but we can also use OpenCV’s machine learning library to make our system more accurate. Moreover, by adding NLP, we can achieve a breakthrough in the field of I/O and get rid of the conventional methods of interaction.

Stay tuned for comparisons between different color models for image processing. Reach out to me if you would like to know more about gesture recognizer.

GitHub Repository at [https://github.com/div5yesh/snapgest](https://github.com/div5yesh/snapgest).

Originally posted: [medium.com/@div5yesh](https://medium.com/@div5yesh/interact-with-computer-using-gestures-opencv-java-ea92198b419d)