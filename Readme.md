## Advanced Lane Finding for Self-Driving Cars
The goal of this project is to produce a robust pipeline for detecting lane lines from raw images captured by camera. The pipeline should output a visual display of the lane boundaries, numerical estimation of lane curvature, and vehicle position within the lane.


### Overview
The steps taken to complete this project are as follows:

* Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
* Apply a distortion correction to raw images.
* Use color transforms, gradients, etc., to create a thresholded binary image.
* Apply a perspective transform to rectify binary image ("birds-eye view").
* Detect lane pixels and fit to find the lane boundary.
* Determine the curvature of the lane and vehicle position with respect to center.
* Warp the detected lane boundaries back onto the original image.
* Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.


#####Camera Calibration
