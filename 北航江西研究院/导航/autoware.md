```
sudo apt update
sudo apt install -y python-catkin-pkg python-rosdep ros-melodic-catkin
sudo apt install -y python3-pip python3-colcon-common-extensions python3-setuptools python3-vcstool
pip3 install -U setuptools
```


```
git clone https://github.com/CPFL/Autoware.git --recurse-submodules
```

```
cd ~/autoware_ws/src
catkin_init_workspace
cd ../
rosdep install -y --from-paths src --ignore-src --rosdistro melodic
./catkin_make_release -j8
```