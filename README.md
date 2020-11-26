# Autoware "Hands-On"

- Graz University of Technology 
- Stanford Lecture AA274 



## Preconditions
- Ubuntu 18.04 (64 bit) is installed --> http://releases.ubuntu.com/18.04/
- ROS (melodic) is installed --> http://wiki.ros.org/melodic/Installation/Ubuntu

# Install autoware by source
(https://gitlab.com/autowarefoundation/autoware.ai/autoware/wikis/Source-Build)

```
sudo apt update
sudo apt install -y python-catkin-pkg python-rosdep ros-$ROS_DISTRO-catkin
sudo apt install -y python3-pip python3-colcon-common-extensions python3-setuptools python3-vcstool
sudo apt install ros-$ROS_DISTRO-lanelet2-*
pip3 install -U setuptools
```

## Create workspace for Autoware.AI
```
mkdir -p ~/ros/autoware.ai/src
cd ~/ros/autoware.ai
```
## Download the workspace configuration for Autoware.AI.
```
wget -O autoware.ai.repos "https://raw.githubusercontent.com/Autoware-AI/autoware.ai/1.14.0/autoware.ai.repos?inline=false"
```

## Download Autoware.AI into the workspace, install dependencies using rosdep and compile it
```
vcs import src < autoware.ai.repos
rosdep update
rosdep install -y --from-paths src --ignore-src --rosdistro $ROS_DISTRO
catkin build --cmake-args -DCMAKE_BUILD_TYPE=Release
```


# Install packages for AA274 lecture
```
git clone https://gitlab.v2c2.at/aa274/aa274_autoware_ws.git ~/ros/aa274_autoware_ws/src
tar -xvf ~/ros/aa274_autoware_ws/src/arg_localization/arg_data_croix_en_ternois/bagfile/devbot_lap0.tar.xz
cd ~/ros/aa274_autoware_ws/src
rosdep install -y --from-paths src --ignore-src --rosdistro $ROS_DISTRO
cd ~/ros/aa274_autoware_ws/
catkin build

```



# Demo Localization
## Terminal 1:
```
roscore 
```

## Terminal 2:
GPS-based localization
```
roslaunch arg_launch Devbot_localization.launch
```
or Lidar-based localization
```
roslaunch arg_launch Devbot_localization.launch lidar_localization:=true
```

# Terminal 3:
```
roslaunch arg_launch Play_rosbag.launch
```



# Demo Path Planning 
# Terminal 1:
```
roslaunch vifware_launch simulation.launch
```

