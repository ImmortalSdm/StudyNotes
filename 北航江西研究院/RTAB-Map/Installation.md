#ROS distribution

```
#18.04
sudo apt install ros-melodic-rtabmap-ros

#16.04
sudo apt-get install ros-kinetic-rtabmap-ros
```


若报错error while loading shared libraries...
```
ldconfig
```
或者
```
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/opt/ros/noetic/lib/x86_64-linux-gnu
```


##从源码构建

已经构建了工作区catkin_ws

```
source /opt/ros/<ROS版本>/setup.bash

source ~/catkin_ws/devel/setup.bash
```

```
sudo apt install ros-noetic-rtabmap ros-noetic-rtabmap-ros

#或删除
sudo apt remove ros-noetic-rtabmap ros-noetic-rtabmap-ros
```