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
sudo apt-get install python-pip
sudo pip install geographiclib
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
rosservice call /fixedwing/param_load_from_file ~/rosflight_ws/param.yml
rosservice call /fixedwing/calibrate_imu
rosservice call /fixedwing/param_write
```

Flip the arm switch on the transmitter.

The airplane should takeoff and fly in an orbit.

### Running and using the Groundstation GUI

**Running**

*Before running for the first time*, see **IMPORTANT NOTE**. Because the GUI receives waypoints at the same time that the plane does, it would be wise to start the ground station before starting the ROSplane simulator. 

Type the following into a terminal:

```
source ~/rosflight_ws/devel/setup.bash
roslaunch ros_groundstation gs_fixedwing.launch
```

**Using**

The fixed wing system will be rendered in real time onto the current map, which can be panned by clicking and dragging. There are four different zoom levels, which can be toggled by scrolling. The *Grid Viewer Mode* checkbox toggles a superimposed grid on the map, which gives positional meter references with respect to the map's origin at all but the outermost zoom level. State values may be compared to their commanded values in the plot widget, which is activated and toggled using the drop-down menu.

ROS subscriber topics can be changed and toggled using the *OPTIONS* popup window. See both tabs to view all the topics that can be modified. By default, *GPS init Subscriber* is disabled. This means that the plane will be rendered with respect to the origin of the selected map, ignoring the actual GPS output of the estimator. If you wish to enable this subscriber, be sure to have a map downloaded whose location actually corresponds to the "location" in the simulator, otherwise the plane will not be visible.

**IMPORTANT NOTE**:

When you run the ground station for the first time, the plugin will parse through the file **map_info.xml**, located in ~/rosflight_ws/src/ros_groundstation. Using the uncommented information, it will proceed to download map tiles for each listed map into the folder ~/.local/share/mapscache. In map_info.xml, each map field must provide a name, center latitude and longitude, and a meter-radius value to tell the parser how much map to download. A normal meter-radius is 1000 meters. The default displayed map is also defined in this file.

By default, only *Brigham Young University* is uncommented as an available map. **Downloading the tiles for a single map will take upwards of 7-8 minutes, so keep this in mind when running for the first time**. After the initial download process, no subsequent access to the internet will ever be needed to use the ground station, unless new maps are uncommented or added.

Each map requires about 1000 images, or 100 MB of space, to render all four zoom levels. In order to download multiple maps in one sitting, the user must obtain an API key from https://developers.google.com/maps/documentation/staticmaps/#api (it takes about 30 seconds to obtain a key).
The key must then be pasted within the file **key.xml**, which is also located in ~/rosflight_ws/src/ros_groundstation. Doing so will allow for downloading up to 25,000 images in a single day without incurring any charge.

