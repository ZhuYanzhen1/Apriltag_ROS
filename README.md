# AprilTags for ROS
***
#### Description: This project is a integration package of Apriltags in ROS(Robot Operating System), which including driver of usb camera, camera calibrator and apriltags detector dependences.
***
#### Computer Environment:
+ CPU: Celeron N2808 @1.58GHz x 2
+ Memory: 4GiB DDR3
+ Operating System: Ubuntu 16.04LTS
+ ROS Version: kinetic 1.12.14
+ Disk: 64GB SSD
***
1. Firstly, install the [apriltag3](https://github.com/AprilRobotics/apriltag "apriltag3") in your system if it isn't installed(I had download it in the directory 'dependency'). You have to install CMake first, switch to the 'dependency' folder, then do:
```
	$ cmake .
	$ sudo make install
```
2. If the dependency is installed successfully, switch to root directory, then do:
```
	$ catkin_make
	$ source devel/setup.sh
```
3. If previous step can be run without error, print out the picture "Calibrate Grid.png", then you can plug in your camera and calibrate it:
```
	$ roslaunch usb_cam usb_cam-test.launch
	$ rosrun camera_calibration cameracalibrator.py --size 7x5 --square 0.02 image:=/usb_cam/image_raw camera:=/usb_cam
```
**cautious: the parameter of --square xxx is the real length of each block of the calibrate grid which you have printed.**

4. Moving and turning the calibrate grid until the "calibrate" button is enabled. Press the "calibrate" button and treat yourself with a cup of tea to wait for the computer to caculate.

5. Then press "Save" button to record the calibrate info and press "Commit" to apply it.

6. Modify the configure file /src/apriltag_ros/config/tags.yaml to set the AprilTags ID and position you prefer to detecte.

7. Launch the detector to publish the info of apriltags:
```
	$ roslaunch usb_cam usb_cam-test.launch
	$ roslaunch apriltag_ros continuous_detection.launch
```
8. Launch Rviz to visualized the location:
```
	$ rosrun rviz rviz
```
Add element "/tag_Odometry" and "/tag_detections_image" as below picture: 
<center> 

![Local View](https://raw.githubusercontent.com/ZhuYanzhen1/Apriltag_ROS/master/Picture/local.png "Local View")
</center> 

Change attribute as below:
<center> 

![Global View](https://raw.githubusercontent.com/ZhuYanzhen1/Apriltag_ROS/master/Picture/global.png "Global View")
</center> 

## Enjoy yourself!