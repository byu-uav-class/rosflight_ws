# rosflight_ws
A full rosplane/rosflight workspace for class demos and getting started

## Getting Started

These instructions will get you a copy of the project up and running on your local machine.

### Prerequisites

You will need to have installed Ubuntu Linux on your computer and have ROS Kinetic intalled and working.

### Installing and Building

Type the following into a terminal

'''
cd ~
git clone https://github.com/byu-uav-class/rosflight_ws.git
cd rosflight_ws
git submodule update --init --recursive
source /opt/ros/kinetic/setup.bash
catkin_make
'''

### Running the ROSplane simulator

Type the following into a terminal

'''
cd ~/rosflight_ws
source devel/setup.bash
roslaunch rosplane_sim fixedwing.launch
'''

Click the play button in the gazebo window toolbar.

### Running the ROSflight sil simulator




