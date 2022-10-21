# ROS Workspace Installation

```
git clone https://github.com/bach05/tiago_theta_ws.git
catkin build
```
# Camera Installation

Follow the steps in this repository: https://github.com/bach05/libuvc-theta-sample.git 

# Running the perception connected to the robot

For each terminal:
```
source /opt/ros/noetic/setup.bash
cd catkin_ws
source devel/setup.bash
export ROS_MASTER_URI=http://10.68.0.1:11311
export ROS_IP=10.68.0.129
```
The `ROS_IP` can be different, depending on the connection. Check it using `ifconfig` onyour PC. 

**Launch the 2D LIDAR people detection:**

Pre-trained models (using PyTorch 1.6) can be found in this [Google drive](https://drive.google.com/drive/folders/1Wl2nC8lJ6s9NI1xtWwmxeAUnuxDiiM4W?usp=sharing). Copy it in the `models` folder. 

Launch:
```
roslaunch dr_spaam_ros dr_spaam_ros.launch
```

**Launch the 3D people tracking:**
The library have been installed in the Tiago internal PC. 

Luanch: 
```
ssh pal@10.68.0.1
roslaunch spencer_people_tracking_launch tracking_personalized.launch laser_bottom:=false
```

**Launch the camera:**

Put camera in LIVE mode and run the driver.
```
cd ~/your_ws/src/theta_z1/libuvc-theta-sample/gst
sh streaming_theta.sh
```
Run the ROS node
```
roslaunch tracking_demo theta_camera.launch 
```
