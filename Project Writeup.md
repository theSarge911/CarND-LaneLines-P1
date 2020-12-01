# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

---

## Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps. 
1. First, I resize the image to 960x540 resolution. This way I can assume a standard size for all kinds of camera. 
2. Second, I convert the image to grayscale. 
3. After that to remove some graininess in the image I use a Gaussian filter with kernel size 5. 
4. After that I use Canny edge detection with lower threshold 50 and upper threshold 150. 
5. For masking I use a simple triangular mask. I decided against using a quadrilateral mask was to avoid some noisy lines that I found while thresholding.
6. After that I use hough lines function with modified draw lines function to get the 2 lines to define my lane.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by first extrapolating all the points to span the region of interest entirely. This can be done by setting y coordinate values and using the slope to find the x coordinates of the end points. This way we will end up with 2 sets of lines. One with positive slope and one with negative slope. We separate out those and take average of all the points of upper endpoints and lower endpoints and draw the lines.


### 2. Identify potential shortcomings with your current pipeline

The major shortcoming of this pipeline is using hard thresholds which are set without any scientific method. Probably no 2 people will arrive at the same threshold this way. This will definitely cause issues when we have different lighting conditions like overcast weather or night time. Also in some frames we don't capture both the lines which can be scary.


### 3. Suggest possible improvements to your pipeline

I believe one possible improvement can be first processing the different colours that are present in the image. Probably finding a way to normalize the colours using images in different lighting conditions. We can use this step first to get an image that is standard for all conditions. Also for capturing lanes I believe we should have cameras that are closer to the road for more clarity in say foggy or very dusty conditions.

I also briefly considered using histogram equalization but it may have very dire consequences in cases when there is a shadow or there are some uneven coloring in the road etc.