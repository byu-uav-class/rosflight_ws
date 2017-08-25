# rosflight_ws
A full rosplane/rosflight workspace for class demos and getting started

## Getting Started

These instructions will get you a copy of the project up and running on your local machine.

### Prerequisites

You will need to have installed Ubuntu Linux on your computer and have ROS Kinetic installed and working.

### Installing and Building

Type the following into a terminal:

```
cd ~
git clone https://github.com/byu-uav-class/rosflight_ws.git
cd rosflight_ws
git submodule update --init --recursive
source /opt/ros/kinetic/setup.bash
catkin_make
```

### Running the ROSplane simulator

Type the following into a terminal:

```
source ~/rosflight_ws/devel/setup.bash
roslaunch rosplane_sim fixedwing.launch
```

Click the play button in the gazebo window toolbar.

The airplane should takeoff and fly a pre-defined waypoint path.

### Running the ROSflight sil simulator

Set up your Taranis QX7 transmitter with a new model. You will probably need to setup a arm switch and reverse your elevator input. Plug the transmitter into your computer with a mini-USB cable.

Type the following into a terminal:

```
source ~/rosflight_ws/devel/setup.bash
roslaunch rosplane_sim rosflight_sil.launch
```

Click the play button in the gazebo window toolbar.

Open another terminal and type:

```
source ~/rosflight_ws/devel/setup.bash
rosservice call /fixedwing/param_load_from_file ~/rosflight_ws/param.txt
rosservice call /fixedwing/calibrate_imu
rosservice call /fixedwing/param_write
```

Flip the arm switch on the transmitter.

The airplane should takeoff and fly in an orbit.


