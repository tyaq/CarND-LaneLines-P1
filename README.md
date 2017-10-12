# **Finding Lane Lines on the Road** 

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report



[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

[image2]: ./test_images_output/solidWhiteCurveEdge.jpg "Edges"

[image3]: ./test_images_output/solidWhiteCurve.jpg "Extrapolate"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps.

1) Convert the images to grayscale.

![alt text][image1]

2) Apply a gaussian blur to smooth out the gradient change over whole image.
3) Use Canny edge detection to find all steep edges in image.
4) Use a Hough transform on an masked region of interest to extract line like features.

![alt text][image2]

5) Draw lines on the image.  

![alt text][image3]
In order to draw a single line on the left and right lanes, I modified the draw_lines() function to average detected lane markings and draw them over the region of interest. I did this by:

1) Determining right or left lane by slope of line. With positive slopes belonging to the the right lane and negative slopes to the left.
2) Averaging all the slopes and intercepts for a side.
3) Plotting the averaged line equation over the region of interest.

### 2. Identify potential shortcomings with your current pipeline

One shortcoming is what happens when in a frame there are no line-like features detected on either side. Then averaging function tries to divide by zero and errors out.
Another shortcoming is Canny/Hough Transform detecting cars and miscellaneous objects inside the region of interest. This ruins the accuracy of the averaged lane lines, and plots them incorrectly.

### 3. Suggest possible improvements to your pipeline

A possible improvement would be to implement a circular buffer to record right and left slopes. Then the averaging function will smooth the lane lines calculations over the course of the video feed. It will also remove the problem of not detecting lanes in frame, as it will show the prior result.

Another potential improvement could be to mask the white and yellow colors in a frame and black out the rest. Then in the canny edge detection would accurately provide only the lane markers in the region of interest.