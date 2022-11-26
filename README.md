# Dataset generation in gazebo

This repository contains code and utilities to generate image data from various PoVs for datasets in a simulated Gazebo environment. The software has been tested with ROS Noetic and Gazebo 11 on Ubuntu 20.04

The repository contains a ROS package gazebo_datagen with the following files

1. launch/drone_world.launch<br>
The launch file will launch a Gazebo environment with a camera model whose model_state can be controlled via Gazebo's ROS API calls. The launch file argument ```world_name``` can be used to modify the world file launched according to requirement.
2. src/set_camera_state.py<br>
The ROS node used to control the sequence of poses of the camera
3. src/utils.py<br>
Utility functions used in set_camera_state.py

### Independent usage

Add the following to your own world file for independent usage.<br>
Some of the common parameters that can be set:
1. initial pose in \<pose>
2. image resolution \<width> and \<height> under \<image>
3. path to save images \<path> under \<save enabled>

```xml
<model name='camera'>
      <static>0</static>
      <pose>-1 0 2 0 1 0</pose>
      <link name='link'>
        <visual name='visual'>
          <geometry>
            <box>
              <size>0.1 0.1 0.1</size>
            </box>
          </geometry>
        </visual>
        <sensor name='my_camera' type='camera'>
          <camera>
            <save enabled='1'>
              <path>/tmp/saved_images</path>
            </save>
            <horizontal_fov>1.047</horizontal_fov>
            <image>
              <width>640</width>
              <height>480</height>
            </image>
            <clip>
              <near>0.1</near>
              <far>100</far>
            </clip>
          </camera>
          <always_on>1</always_on>
          <update_rate>0.1</update_rate>
        </sensor>
        <self_collide>0</self_collide>
        <inertial>
          <pose>0 0 0 0 -0 0</pose>
          <inertia>
            <ixx>1</ixx>
            <ixy>0</ixy>
            <ixz>0</ixz>
            <iyy>1</iyy>
            <iyz>0</iyz>
            <izz>1</izz>
          </inertia>
          <mass>1</mass>
        </inertial>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
    </model>
```


> Date of completion: July 2022