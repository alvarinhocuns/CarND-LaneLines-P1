# **Finding Lane Lines on the Road** 

## Álvaro Dosil Suárez

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/step1.jpg "Grayscale"

[image2]: ./test_images_output/step2.jpg "Filtered"

[image3]: ./test_images_output/step3.jpg "Edges"

[image4]: ./test_images_output/step4.jpg "Interesting"

[image5]: ./test_images_output/step5.jpg "Detection"

[image6]: ./test_images_output/step6.jpg "Extrapolation"

[image7]: ./test_images_output/step9-result.jpg "Result"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 9 steps, that were increased to 11 steps to work on videos.

I created a function called DetectLines() where I included all the steps. These steps are:

# 1) Convert image to gray scale

![alt text][image1]

# 2) Apply a gauss filter to remove noise

![alt text][image2]

# 3) Detect borders using canny edge detection

![alt text][image3]

# 4) Select only the interesting region of the image

![alt text][image4]

# 5) Detect lines in this region using the Hough transform

![alt text][image5]

# 6) Extrapolate the detected lines to the whole interesting region

![alt text][image6]

# 7) Divide the lines in two side groups

# 8) Remove the outliers with the m or b parameters 3sigma away from the mean

# 9) Average the lines

![alt text][image7]


# Additional steps
Moreover, as I already mentioned, in order to work with the videos I included two more steps.

After processing the videos, the obtained lines showed a very nervous behavior because of the refresh frequency. Furthermore, in very tiny instants, the system cannot find some lines. To avoid this I created a low frequency pass filter that averages the result of the more recent results.

Furthermore, my pipeline didn't work in the challenge video. To fix that I included a step where I select the white and yellow parts of the image. Then I mask the obtained image with the initial one and add the result to the pipeline. Doing this, I get a much better performance on the challenge video, nevertheless the result is a little bit more poor in "solidWhiteRight.mp4" and "solidYellowLeft.mp4". 


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be when the pipeline should have to work with blue lines or in rainy conditions. I detected that my code is very sensitive to the different colors on the road.
Moreover, I haven't checked what happens when the car finds marks in between the two lines (out of the scope of this exercise). Probably it will detect new lines that in the best case would be removed by the removeOutliers() function or smoothed by the filter, and in the worse scenario they would create fake final lines.


### 3. Suggest possible improvements to your pipeline

An improvement needed is firstly to fine tune the pipeline. I was trying different tunes to detect a wide range of white colors rejecting the road colors, but it was impossible to obtain a better result than the shown in the notebook.
