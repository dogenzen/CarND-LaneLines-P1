# **Finding Lane Lines on the Road**
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

Overview
---

When we drive, we use our eyes to decide where to go.
The lines on the road that show us where the lanes are act as our
constant reference for where to steer the vehicle.  Naturally, one of
the first things we would like to do in developing a self-driving car
is to automatically detect lane lines using an algorithm.

In this project we will detect lane lines in images using
Python and OpenCV.  OpenCV means "Open-Source Computer Vision",
which is a package that has many useful tools for analyzing images.

**The goals / steps of this project are the following:**

* Make a pipeline that finds lane lines on the road
* Reflect on the work here as a written report

The pipeline code to find lane lines on the road is implemented in P1.ipynb (jupyter notebook format). 

## Reflection

The pipeline consists of **five** image transformation steps as described below:

> **Grayscale --> Blur --> Edges --> Region-of-Interest --> Lines**

1. **Grayscale conversion:** initially the image is converted to grayscale in order to preapre it for further processing.
2. **Gaussian Blur:** then the image is blurred and smoothened in order to remove any noise.
3. **Detect Edges:** in this step, *Canny edge detection* algorithm is applied to find edges (pixes with highest gradient) in the image.
4. **Define a region of interest:** then a region of interest, part of the image that includes only the edge of the road, is defined to exclude areas that will not have lanes in it.
5. **Detect Lines:** finally, **Hough transfromation algorithm** is applied to find lines in the region of interest.

The lines detected by the above pipeline are rendered on top of the image.

### Challenges
There are still a few potential shortcomings of the above pipeline that needs to be considered. 
One of the shortcoming is when there are no clear edges that can be identified by the edge detection algorithm due to the lane or road color. Another shortcoming could happen due to other lines that can form due to multiple lanes, cracks etc.

### Improvements

A possible improvement would be to consider the slopes to eliminate extraneous lines. When a lane is not detected, a few previous frames could be considered to extrapolate but the pipeline has to be robust to not over compensate for more than a couple frames. A moving average of lines over certain number of frames could be computed to keep the detetcted lane lines to smoothen, especially when the lanes turn.