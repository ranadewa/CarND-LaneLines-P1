# **Finding Lane Lines on the Road** 

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

---

### Reflection

### 1. Pipe line description
 |  | |
 |-------|----|
 |1. Original | 2. Greyscale|
 |<img src="test_images_output/pipeline/1%20original.png" width="500"/>|<img src="test_images_output/pipeline/2%20greayscale.png" width="500"/>|
 |3. Color Mask applied | 4. Area of interest defined|
|<img src="test_images_output/pipeline/3%20color%20mask%20applied.png" width="500"/>|<img src="test_images_output/pipeline/4%20area%20of%20interest%20taken.png" width="500"/>|
|5. Gaussian blur applied| 6. Canny Edge detection applied|
|<img src="test_images_output/pipeline/5%20gaussian%20blurred.png" width="500"/>|<img src="test_images_output/pipeline/6%20canny%20applied.png" width="500"/>|
|7. Averaged Hough lines to get best fit| 8. Best fit draw on image|
|<img src="test_images_output/pipeline/8%20best%20line%20fitted.png" width="500"/>|<img src="test_images_output/pipeline/9%20line%20drawn%20on%20the%20image.png" width="500"/>|


<img src="test_images_output/pipeline/7%20coordintate%20from%20hough%20line%20detection%20and%20the%20best%20fit%20line.png" width="200"/> <br>
My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I .... 

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
