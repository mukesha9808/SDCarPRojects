# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.



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

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I used gaussian function for smoothening of image. After that Canny edge detection method is used for detecting edges, then region of interest is defined. I used trapezoid for region of interest.  I kept region of interset a bit away from vehicle to avoid edges due to reflection. Hough transformation is performed within region of interest.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function as following
for each line in lines
    calculate slop and bias of line
     line is considered for valid left line if
         slope < -0.5 
         and x1 and x2 are in left half of image
         and |LeftLine_MeanSlope- cureentline_slope| < 0.2 (First entry will ignore this condition)
     once valid left line is found
         calculate mean slope and bias for left line
     line is considered for valid right line if
         slope > 0.5 
         and x1 and x2 are in right half of image
         and |RightLine_MeanSlope- cureentline_slope| < 0.2 (First entry will ignore this condition)
     once valid right line is found
         calculate mean slope and bias for right line
    Once slope and bias for left and right line found, find x values for y=0.65*imageHeight and y=imageHeight
    Draw line using new x and y pairs     
            

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be handling shadows. if shadow of tree or pole is such that it passes the left line and right line creteria but then it may not work correctly. Also if lime marking are light then edge might not be detected at all.



### 3. Suggest possible improvements to your pipeline

A possible improvement would be to improve edge detection for line consistently even if markings not very clear.
