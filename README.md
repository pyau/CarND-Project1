#**Finding Lane Lines on the Road** 

---

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps.

1. I create a mask of only lane lines by filtering out the grey road.
2. I applied grayscale to my image.
3. I apply gaussian blur with kernel size of 7.
4. I apply canny edge detection.
5. I found the region of interest by masking out the area that does not include the lane lines.
6. I found and draw hough lines.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by first eliminating some noise that definitely do not fit as lane line, i.e. very close to be a horizontal line or vertical line.  Then I separate the remaining lines by positive and negative slope.  Once I separate all the points into two categories, I fit a straight line to the points that define the lines.  Then I draw the positive and negative sloped lines as the two lane lines, and mask out the excessive length of the lines. 


###2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the car is going through a 90 degree turn.  I chose to eliminate horizontal and vertical lines in draw_lines() function so the program works better for the sample videos only.

Changing lane would create another trouble.  I masked out all the other lanes before processing the images. A more complete solution should be able to map out different lanes in the environment.

###3. Suggest possible improvements to your pipeline

A possible improvement would be to fine tune the values for my step 1: Creating a mask of showing only lane lines.  My processing pipeline currently cannot find the lane lines correctly for the whole duration of the challenge video.  But I believe it’s a matter of spending more time tuning the parameters in my code’s mask_color() function.

Another potential improvement could be to fine tune the values used for hough transform and canny edge detection.  For most of the time, the parameters that I used can detect the correct lane lines.  However, there is still several frames that the lane lines aren’t drawn exactly on the lanes themselves.  I believe my parameters still generate too much false positives, e.g. left side of the lane section gets connected to the right side of the lane section.

Another easy improvement to do is to average out the lane lines across several frames, to make the presentation smoother. However, I question about this method because the information display might be delayed, in the case of sudden changes (e.g. sharp turns).
