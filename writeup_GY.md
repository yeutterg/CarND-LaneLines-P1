**Finding Lane Lines on the Road**

By Greg Yeutter
2017-02-21

---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consists of the following steps: 
1. Converting image to grayscale
2. Applying a Gaussian blur to the image
3. Applying Canny edge detection
4. Masking the image so that only the region of interest is processed
5. Running the Hough transform to identify lines
6. Converting those lines into straight lines
7. Smoothing the result with a moving average filter
8. Plotting the lines on top of the image

In order to draw a single line on the left and right lanes, I created the function draw_straight_lines().
This function works as follows:
1. Separate the right and left line based on their slope
2. Average the line ending x,y coordinates for each side
3. Calculate the slope and intercept of each average line
4. Using the slope and intercept, extend the lines to the bottom and apex of the lane
5. Update the moving average of the last few lines and the new lines
6. Plot the moving average lines


###2. Identify potential shortcomings with your current pipeline

While this pipeline works on the first two videos, I am getting a float infinity error on the optional third video. Some tweaking will be required. If I figure this issue out, I will resubmit.

In low-contrast situations, the line identification pipeline may not work well.

At intersections with sharp angles, the code cannot draw over the entire lane marking.


###3. Suggest possible improvements to your pipeline

One improvement would be cleaner code. This project required a lot of tweaking and hacking to get the desired result, and although I commented frequently, the codebase could absolutely be smaller and more consistent stylistically.

Another improvement would be removing global variables in favor passing average values in a functional programming manner.

If matrix math (NumPy) was used more often, this code could probably be more efficient and compact. However, we might be getting into premature optimization territory.

The optimal parameters for Gaussian smoothing, the Hough transform, moving average, etc. might be different based on the input video. A more advanced pipeline could self-calibrate based on the observed quality of lane identification. Some ML could be used here.