# **Finding Lane Lines on the Road** 

## Writeup

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

---

### Reflection

### 1. Pipeline description.

My pipeline consisted of 5 steps:

Step1: converted the images to grayscale
Step2: Apply Gussian smoothing on the gray image
Step3: Carry out Canny to detect the edges
Step4: Apply Hough line detection to detect lines
Step5: Caculate the final two lanes according to the output of hough line detections, then draw lanes on image.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by divide the lines returned from hough_lines() by their slope, only remain lines whose slope is between 0.5 and 3 as the left lines, lines with slope between -3 and -0.5 as right lines, then calculate the average of left lines and righe lines respectively. consider the final two average lines as the final detected left and right lane.

Also, in some cases, the hough_lines() can't detected any left lines or right lines, or neither. Consider these situation in the algorithm and just pass them, which means currently my implemntation will not draw corresponding lane in this situation.

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![One example of the lanes detection][/test_images_output/solidYellowLeft.jpg]


### 2. Potential shortcomings with current pipeline


One potential shortcoming would be what would happen when line with the required slope but occurred far away with the actual lane was detected within interest region. This will cause the final caculated lane bias to the actual lane. That's why for the "Optional Challenge" section, mostly my recognizing implementation works well, but in some frames the above situation occurs, then the output lane shifts a lot.

Another shortcoming could be happen when car start with a situation that the car is not parallel with the actual lanes, it might be that the two lanes' slope are both >0 or <0.

### 3. Suggest possible improvements to your pipeline

A possible improvement would be to change the current average caculation to a average caculation with weight that according to the lines' length.

Another potential improvement could be to trying to filter out the detected lines with "correct" slope but shift to the actual lane, although for this I didn't have new ideas for now...
