# Advanced Lane Finding for Self-Driving Cars
The goal of this project is to produce a robust pipeline for detecting lane lines from raw images captured by camera. The pipeline should output a visual display of the lane boundaries, numerical estimation of lane curvature, and vehicle position within the lane.


## Overview
The steps taken to complete this project are as follows:

* Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
* Apply a distortion correction to raw images.
* Use color transforms, gradients, etc., to create a thresholded binary image.
* Apply a perspective transform to rectify binary image ("birds-eye view").
* Detect lane pixels and fit to find the lane boundary.
* Determine the curvature of the lane and vehicle position with respect to center.
* Warp the detected lane boundaries back onto the original image.
* Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.


#### Camera Calibration

Cameras introduce distortion to images. Two major kinds of distortion are radial distortion and tangential distortion.
Radial distortion causes straight lines to appear curved. Radial distortion becomes larger the farther points are from the center of the image. Similarly, tangential distortion occurs because the image-taking lense is not aligned perfectly parallel to the imaging plane. So, some areas in the image may look nearer than expected. 
I started by preparing "object points", which will be the (x,y,z) coordinates of the chessboard corners. The provided sample images of chessboards are fixed on the (x,y) plane at z=0, such that the object points are the same for each calibration image. Thus, objp is just a replicated array of coordinates, and objpoints will be appended with a copy of it every time all of the chessboard corners are successfully detected in a sample image. With each successful chessboard detection, imgpoints will be appended with the (x,y) pixel position of each of the corners. I then used the output objpoints and imgpoints to compute the camera calibration and distortion coefficients using the OpenCV calibrateCamera() function. The resulting camera matrix and distortion coefficients are then used to undistort images using the OpenCV undistort() function. Here an original image (left) and an undistorted image (right):

<img src="https://user-images.githubusercontent.com/103825664/219966068-e291dbe0-99c9-4960-a7a5-fb86b06758fc.jpg" width="420" height="240"> <img src="https://user-images.githubusercontent.com/103825664/219966217-ab3a1e80-0fc2-4195-8633-8c46e7e80af5.jpg" width="420" height="240">
