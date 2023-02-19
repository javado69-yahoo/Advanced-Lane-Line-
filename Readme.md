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

### Distortion Correction


Using the camera matrix and distortion coefficients produced in the previous step, I undistort all incoming raw images using the OpenCV undistort() function.
Notice the **white car** for an example.

<img src="https://user-images.githubusercontent.com/103825664/219967350-6bca29ac-750f-4381-ba37-98a41879a693.jpg" width="420" height="240">  <img src="https://user-images.githubusercontent.com/103825664/219967373-2c9f56da-72af-4105-91a7-f5183d272764.jpg" width="420" height="240">

### Color and Gradient Threshold
In order to accurately find the lane lines in an image, I applied a number of thresholding techniques to filter out potential noise (such as shadows, different color lanes, other cars, etc). From the course and training the S channel is doing a fairly robust job of picking up the lines under very different color and contrast conditions, while the other selections look messy. The R channel in RGB does rather well on the white lines, perhaps even better than the S channel in HLS. AS a result I combined S channel with Red channel tresholds which the reuslt for R and S are as follow (R channel (left) and the S channel (right)):


<img src="https://user-images.githubusercontent.com/103825664/219969697-2574f001-8088-42e8-8361-586012f0390b.jpeg" width="420" height="240">  <img src="https://user-images.githubusercontent.com/103825664/219969728-ab21b214-299a-4661-a700-9e100443f3f5.jpeg" width="420" height="240">

