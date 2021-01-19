https://www.ncnynl.com/archives/201911/3482.html

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
rosdep update
rosdep install -y --from-paths src --ignore-src --rosdistro melodic
```



