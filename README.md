# ROS2 Driver for Rover Robots
## About:
- This package is exclusively built for ROS2. It is being tested on Ubuntu 22.04 and ROS2-Humble.
- This is built on top of the old roverrobotics_ros2 driver. It is designed specifically to fix many reoccuring bugs that we faced with the old driver.
- This driver is very much so in the development and beta stages. Please report any issues that you face so we can create a stable release.

## Roadmap / To-Implement:
1) Restructuring of Launch files
	- Our goal is to make it more organized and easier to launch various packages
2) Out of the box SLAM and Nav2
	- With autonomous robotics growing in popularity we feel it is important to be able to provide a out-of-the-box solution so our customers can open the box and have SLAM and Nav2 running in no time
3) Foxglove implementation ([Foxglove](https://foxglove.dev/))
	- We have found foxglove to be a very useful tool while developing. In order to provide this out-of-the-box to our customers we will be implementing an automated launch (if chosen on install) of foxglove_bridge so you can easily connect and visualize your robot data.
4) Better diagnostics
	- When I came onto rover, it was very hard for me to diagnose issues with the robots.
	- My goal is to provide thorough diagnostics that make it easy to tackle any problem that arises.
5) New controller driver
	- Our current controller driver presents some issues when running over can causing jittering. A new controller driver / fixed driver is in the works.
6) URDF Meshes and Simulation Support
	- Simulation is an important part of robotics prototyping and we aim to provide the tools necessary to get up and running quicker and easier
7) Updated documentation and tutorials
	- We want our robots to be used for both research and education. It is important that we can provide accurate, up-to-date, and easy to follow documentation to help our users get started and understand the different aspects of ROS and our robots.

## Installation instructions - Outdated (Do Not Follow)

1. Cloning this repository into your workspace
```
cd workspace/src/
git clone https://github.com/RoverRobotics/roverrobotics_ros2.git
```
2. Install Udev rules for robot
```
cd workspace/src/roverrobotics_driver/udev
sudo cp 55-roverrobotics.rules /etc/udev/rules.d/55-roverrobotics.rules && sudo udevadm control --reload-rules && udevadm trigger
```
3. Install shared library
``` 
cd ~/
mkdir library/
cd library/
git clone https://github.com/RoverRobotics/librover
cd librover/
cmake .
make
sudo make install 
```
4. Rebuild your workspace
```
cd workspace/
colcon build
```
5. Update env variables and configuration files 
```
source install/setup.sh
```
6. Launch Robot (replace <launch file name> with your robot config.)
```
ros2 launch roverrobotics_driver <launch file name>
```
  ```
  Launch Files:
  <model>.launch.py: Launches robot configuration for specific rover robot. (i.e. Mini, Mega, Pro2, Zero2)
  <model>_teleop.launch.py: Launches robot configuration with teleop controller enabled.
  rover_slam_mapping.launch.py: Launches lidar and slam toolbox in asynchronous mapping mode(Requires slam package).
  rover_slam_localization.launch.py: Launches lidar and slam toolbox in localization mapping mode.
  ```
