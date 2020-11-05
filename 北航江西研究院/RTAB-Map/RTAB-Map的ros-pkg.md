装好ROS后

确认已设置工作空间
```
echo $ROS_PACKAGE_PATH
```
得到

`/home/tx2/catkin_ws/src:/opt/ros/melodic/share`

---

安装rtabmap-ros
```
sudo apt install ros-melodic-rtabmap ros-melodic-rtabmap-ros
```

---

可选依赖

若要使用SURF/SIFT，则
```

```

g2o
```
sudo apt install ros-melodic-libg2o
```


GTSAM
```

```


---

安装RTAB-Map独立库


```
cd ~
git clone https://github.com/introlab/rtabmap.git rtabmap
cd rtabmap/build
cmake ..  -DCMAKE_INSTALL_PREFIX=~/catkin_ws/devel
make
sudo make install
```

---

安装RTAB-Map ros-pkg


```
cd ~/catkin_ws
git clone https://github.com/introlab/rtabmap_ros.git src/rtabmap_ros
catkin_make -j1
```

可选：

`Add -DRTABMAP_SYNC_MULTI_RGBD=ON` to `catkin_make` 如果你计划使用多相机

`Add -DRTABMAP_SYNC_USER_DATA=ON` to `catkin_make` if you plan to use user data synchronized topics.





