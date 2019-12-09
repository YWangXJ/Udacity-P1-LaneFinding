# Finding Lane Lines on the Road


Overview
---

The goals of this project is to:
- Create pipeline to detect lane lines on the road from images or videos
- Write reflection to describe the current pipeline, identifies its potential shortcomings and suggests possible improvements.


Pipeline
---

The pipeline consisits of steps with functions
- **grayscale**: returns a gray scaled image using **cv2.cvtColor** method.
- **gaussian_blur**: apply gaussian blur **cv2.GaussianBlur** that returns a smoothed image for the better performance of edge detection.
- **canny**: returns edges using the Canny transform **cv2.Canny**.
- **region_of_interest**: takes outputs from **canny** and returns ROI that are formed by 4 vertices
- **hough_lines**: Use Hough transformation to find the lines on the masked image using **cv2.cv2.HoughLinesP**.**average_slope_intercept** and **make_line_points**  are used to find the average slopes and intercepts of detected hough lines.
- **weighted_img**: draw lines generated from **hough_lines** on the original image with adjustable transparance

In order to draw a single solid line on the left and right lanes, I modified the **hough_lines** function by adding **average_slope_intercept** and **make_line_points** function.**average_slope_intercept** takes lines from **hough_lines** and returns the average slopes and intercepts of left and right line, respectively; **make_line_points** converts lines into pixel points that will be used in **draw_lines**.

Shortcomings and Possible Improvements
---
- Lines vibrates a lot. Countermeasures: A smoothing method can be implemented between video frames.
- Some white points such as poles or litters can be detected as lane marks sometimes. Countermeasures: 1. if slopes of lines change a lot between two consecutive video frames, the deviation should be considered as error and removed.
- I tried to implement the pipeline into the **challange.mp4** but noticed that the size and coordinates orientation is different from the previous videos. This means that the developed method may be only good for the same video size 
