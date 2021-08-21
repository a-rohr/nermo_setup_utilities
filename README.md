This package contains some valuable utility resources and scripts for interacting and testing Nermo.

These resources make use of the fact that the RPi of Nermo is connected to the main ROS Master of the master PC by setting the correct ROS_MASTER_URI.

On Nermo, the low_level_controller node is listening on the ROS_TOPIC = "q_values" for the input commands of the servos.

# IMPORTANT
The topic "q_values" is of type std_msgs/Float32MultiArray of size 12 in the unit type radians (conversion to degrees occurs on the low_level_controller). The Float32 data[12] addresses the individual servos in the following order.

data = [front_left_shoulder, front_left_elbow, front_right_shoulder, front_right_elbow, rear_left_hip, rear_left_knee, rear_right_hip, rear_right_knee, tail, neck_pan, head_tilt, spine_horizontal_flex]

For the current implementation, the spine_vertical_flex has been omitted (not being used). In future iterations, the "q_values" Float32 data[] would be extended to size 13, as follows: 

data = [front_left_shoulder, front_left_elbow, front_right_shoulder, front_right_elbow, rear_left_hip, rear_left_knee, rear_right_hip, rear_right_knee, tail, neck_pan, head_tilt, spine_horizontal_flex, spine_vertical_flex]

## 1 Testing Servo Motors of Nermo
To quickly test the servo motors (debugging and checking neutral positions to align with the simulation) the ROS package rqt_ez_publisher from "here" can be used. 

Install the rqt_ez_publisher package in the catkin workspace via git clone - making sure to pick the correct ROS version.
Then run the rqt_ez_publisher (after starting all other nodes) using the following command:
rosrun rqt_ez_publisher rqt_ez_publisher

Then load the configuration file (by clicking on the "settings" icon) from the "resources" folder of this package called "q_values_template_ez_publisher.yaml". 

This should load up 12 sliders - one slider for each of the 12 servo in the Float32 data[] of "q_values". Now each servo can be addressed and tested individually using the sliders.