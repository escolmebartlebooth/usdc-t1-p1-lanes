# Udacity Self-Driving Cars Nanodegree: Term 1: Project 1: Detecting Lane Lines

## Overview

The project called for a lane detection pipeline to be created which could take in images of cars on highways and apply road lane lines to the image for the lane the car is in. Then later to apply that pipeline to videos of the car driving.

The main challenges to complete the project were:

+ creating averaged lines for left and right lanes
+ smoothing the lines between frames on the video to reduce jitter
+ attempting to apply the pipeline to more challenging videos

The project write up can be found in usdc_t1_p1_bartlebooth.md

## Pre-Requisites

The major pre-requisites for this project are:

+ Python 3 Installation
+ Numpy, OpenCV, matplotlib and their dependencies
+ moviepy
+ package versions can be found in packages.txt

## Implementation Notes

The pipeline consists of a lane-detection class which when instantiated can be used to call Process_Image(), supply the image to process. This then calls the following pipeline:

+ create a grayscaled, blurred image
    + call output_type = 'blurred' to stop at this point and return the blurred image
+ create an image of detected edges using the canny function
    + call output_type = 'edges' to stop at this point and return the edged image
+ create a region of interest and mask the edged image to that region:
    + call output_type = 'masked' to stop at this point and return the masked image
    + set up the lane detector prior to calling Process_Image() with the extent of the region of interest - default values work well with supplied images and test videos
+ create an image with lines drawn on the image, using hough transform to detect the line segments:
    + call output_type = 'masked_segments' to stop at this point and return the lane segments drawn on the masked edged image or...
    + call output_type = None to finish the pipeline, average the negative and positive lines into 1 each and to extrapolate the final lines

It is possible to change various parameters in the code (as noted in the code) to alter aspects of the processing.