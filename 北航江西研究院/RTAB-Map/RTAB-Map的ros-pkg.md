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








