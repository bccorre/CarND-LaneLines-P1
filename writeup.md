# **Finding Lane Lines on the Road**

## Project 1 Writeup

### Name: Bruno C. Correa

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_out/solidWhiteCurve.jpg "pipeline result example"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 7 steps. First, I converted the images to grayscale, then I applied a gaussian blur,  call the canny edge function, selects the region of interest (a trapezoidal region), define the parameters to apply hough line algorithm, and then combine the original image with the line of the hough transform algorithm, to finally rescale the image in order to pixel stay between 0 and 255 values.

The draw_lines function first loop through the line of the hough transform algorithm, and select the ones that has slopes less than -0.6 (classified as part of the left line) and greater than 0.55 (pertaining to the right line). Right after, a linear interpolation is done through the points of the left line and the extreme points are determined, basically the ones that has maximum y and minimum y considering the region of interest, to finally draw the line considering this two extreme points. The same operation is done to the right line.

Below follows a result of this algorithm:

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


There are many shortcomings in this algorithm:

1- the calculated lines does not consider curves of the road, it uses linear interpolation
2- result image is not smooth as in the example of the problem, there is a jitter that need to be removed


### 3. Suggest possible improvements to your pipeline

There are many possible improvements, but considering the shortcomings listed above I will list possible solutions to them:

1- considering polynomial of higher order for the interpolation
2 - consider smooth the lines between frames of the video, it is necessary to make a history of the past frames
