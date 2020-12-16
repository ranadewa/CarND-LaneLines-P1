# **Finding Lane Lines on the Road** 

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

---

### Reflection

### 1. Pipe line description
  The implemented pipe line has following steps.  
  #### Step 1: Convert image to greyscale  
  This is done to converge (R,G,B) channels to one channel which would be used as primay image for further processing. Lane lines have bright colors and the resulting grey image would have higher pixel values for lane lines.
  #### Step 2: Apply color mask
  In order to extract brighter lane lines a color mask is applied which would filter out lower pixel values from the image.
  #### Step 3: Define area of interest
  Since the image can have brigher colors in other areas (sky, cars, sign boards) as well an area of interest is defined which closely encircles the road. This filters out other higher value pixels from the image. 
  #### Step 4: Use Canny edge detection
  Gaussian blurring is applied on above image to reduce the noice and then canny edge detection is done to get points which has the highest gradient change. The result would have non zero pixel along the edges in the image. 
  #### Step 5: Use HoughLine generation on detected edges
  The result from the above step is fed to HoughLine generation function which returns lines (two coordinate points) matching the generation crietieria. These line segments which are aligned with the lane lines are then used to derive the best fit line using ```draw_lines()``` function. How it works is defined [here](https://github.com/ranadewa/CarND-LaneLines-P1/blob/master/writeup_template.md#draw_lines-function-enhancement).

  #### Step 6: Draw best fit lines on the original image
  The best fit lines are drawn on the original image.

 ### Pipeline in action
 Given below are images at each stage of the pipeline.
 |  | |
 |-------|----|
 |a. Original | b. Converting to Grey Scale (Step 1) |
 |<img src="test_images_output/pipeline/1%20original.png" width="500"/>|<img src="test_images_output/pipeline/2%20greayscale.png" width="500"/>|
 |c. Color Mask applied (Step 2) | d. Area of interest defined (Step 3)|
|<img src="test_images_output/pipeline/3%20color%20mask%20applied.png" width="500"/>|<img src="test_images_output/pipeline/4%20area%20of%20interest%20taken.png" width="500"/>|
|e. Gaussian blur applied (Step 4)| f. Canny Edge detection applied (Step 4)|
|<img src="test_images_output/pipeline/5%20gaussian%20blurred.png" width="500"/>|<img src="test_images_output/pipeline/6%20canny%20applied.png" width="500"/>|
|g. Averaged Hough lines to get best fit (Step 5)| h. Draw best fit on image (Step 6)|
|<img src="test_images_output/pipeline/8%20best%20line%20fitted.png" width="500"/>|<img src="test_images_output/pipeline/9%20line%20drawn%20on%20the%20image.png" width="500"/>|

#### ```draw_lines()``` function enhancement
This function is fed with the generate Hough lines. Each Hough line is represented by two coordinate points. First these lines are sparated as left line lane or right line lane by checking the gradient. Left lane has a positive gradient with _x-axsis_ whereas right lane has a negative gradient. 
```python
    for line in lines:
        for x1,y1,x2,y2 in line:
            
            m = (y2-y1)/(x2-x1)
            
            if(invalidGradient(m)):
                continue
            elif(m > 0): # left line
                selected_lines = left_lines
            else :
                selected_lines = right_lines
            
            selected_lines[0].append(x1)
            selected_lines[0].append(x2)
            selected_lines[1].append(y1)
            selected_lines[1].append(y2)
```
After above seperation the best fit line for the coordinates is calculated using numpy's polyfit function for a 1st degree polynomial.
```python
m, b = np.polyfit(lines[0], lines[1], 1)
```
The coordinates and the best fit line through them can be show as below.
<img src="test_images_output/pipeline/7%20coordintate%20from%20hough%20line%20detection%20and%20the%20best%20fit%20line.png" width="500"/> <br>
In some cases the left lane can have Hough lines which might have a small negative gradient or vice versa. In order to avoid these kind of scenarios a gradient validation function is defined.
```python
def invalidGradient(m):
    return abs(m) < 0.5 or abs(m) > 0.8
```
The values for upper and lower bound of this function is decided by looking at the emperical values returned by the np.polyfit funtion for the test image set.
```
solidWhiteCurve.jpg
grad: 0.5667955203478112, inters: 36.602850952764314
grad: -0.785788343871845, inters: 684.7752908608066
solidWhiteRight.jpg
grad: 0.6457502258798224, inters: -2.0708338799410453
grad: -0.7075461250526038, inters: 647.7610910540652
solidYellowCurve.jpg
grad: 0.63282941446994, inters: 6.458938557458027
grad: -0.7292760194350086, inters: 660.0234748806068
solidYellowCurve2.jpg
grad: 0.6076113853953671, inters: 17.385199297656346
grad: -0.7323791683315588, inters: 660.588457247526
solidYellowLeft.jpg
grad: 0.6292965724244773, inters: 4.1443924975099735
grad: -0.7113211226573143, inters: 646.0804852753902
whiteCarLaneSwitch.jpg
grad: 0.5858636347530163, inters: 27.226907756173247
grad: -0.7840469091940641, inters: 688.7358580237942
```

### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
