https://www.ncnynl.com/archives/201903/2884.html

---

```
sudo apt-get install ros-melodic-kobuki-*
sudo apt-get install ros-melodic-ecl-streams
sudo apt-get install libusb-dev
sudo apt-get install libspnav-dev
sudo apt-get install ros-melodic-joystick-drivers
sudo apt-get install bluetooth
sudo apt-get install libbluetooth-dev
sudo apt-get install libcwiid-dev
```

---


```
roslaunch turtlebot_bringup minimal.launch

roslaunch turtlebot_teleop keyboard_teleop.launch
```


---





#### ‘shared_ptr’ in namespace ‘std’ does not name a template type

add in that package's CMakeLists.txt 

```
add_compile_options(-std=c++11)
```

#### ‘nullptr’ was not declared in this scope

```
sudo gedit ~/turtlebot_ws/src/kobuki_controller_tutorial/CMakeLists.txt
```
add
```
add_compile_options(-std=c++11)
```

#### ‘shared_ptr’ in namespace ‘std’ does not name a template type




---
