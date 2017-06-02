# **Finding Lane Lines on the Road** 

## Writeup for Fining Lane Project

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps. First, I read in the file using for loop for all the image files under the folder of "test_images" then converted the images to grayscale. Second, I defined the kernel size 3 and applied Gaussian smoothing to the grey scale image. Third, I define the parameters (lower threshold and upper threshold) for Canny edges and apply. Fourth, I created a masked image to only keep the region of the image defined by the polygon. Fifth, I defined the Hough transform parameters and returned the image with hough lines drawn. At last, I drew the line on the original image and save the images to the same folder.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function as follows: First, creating empty arrays for right slop, right center, left slope and left center. Second, for all the line segments from Hough transformation, separating the segments for right slope if the slope ((y2-y1)/(x2-x1)) is greater than 0.4, and for left slope if the slope is less then -0.4. Save the slope and segment center to both left and right side. Third, calculating the average of right slopes and left slope, also the average of left center and right center. Fourth, using the average center and slope information, the y coordinate of the line starting point imshape[0]*0.58 and y coordinate of the line ending point imshape[0], I calculated the x coordinates of the line starting and ending points for both sides. At last, I draw the lines using the line starting and ending points for both sides.

After applying the pipeline descrbibed above, here is the image I got (please see all the image files starting with "output" in the name)

### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming is that the current line starting point y coordinates for both left side and right side is imshape[0]*0.58, which could be not accurate if the lanes are curved a lot in the image or the lanes are shorter in some images.

Another potention shortcoming is that 0.4 and -0.4 are the current thrsholds for the slopes to compare to determine the line segment is left side or it is right side. In some extreme cases, these threshold would be problematic if the line segment is very flat in the picture.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to have adjustible y coordinates for the line starting points based on the image
