```
git clone https://github.com/unr-arl/mbplanner_ws.git

cd mbplanner_ws
git checkout melodic-devel

wstool init
wstool merge packages_https.rosinstall
wstool update

catkin config -DCMAKE_BUILD_TYPE=Release
catkin build
```

```
roslaunch mbplanner mbplanner_m100_sim.launch
```

---

# error



error: ‘CV_LOAD_IMAGE_GRAYSCALE’ was not declared in this scope
    covariance_image_ = cv::imread(image_name, CV_LOAD_IMAGE_GRAYSCALE);


opencv4不再使用旧的CV_LOAD_IMAGE_GRAYSCALE等几个参数，需要修改为其对应的参数
```
sudo gedit /home/zbxavier/mbplanner_ws/src/sim/rotors_simulator/rotors_gazebo_plugins/src/gazebo_odometry_plugin.cpp
```
cv::Mat m = cv::imread(filename, CV_LOAD_IMAGE_GRAYSCALE);
改为
cv::Mat m = cv::imread(filename, cv::IMREAD_GRAYSCALE);

cv::Mat m = cv::imread(filename, CV_LOAD_IMAGE_COLOR);
改为
cv::Mat m = cv::imread(filename, cv::IMREAD_COLOR);

cv::Mat m = cv::imread(filename, CV_LOAD_IMAGE_UNCHANGED);
改为
cv::Mat m = cv::imread(filename, cv::IMREAD_UNCHANGED);

---

/home/zbxavier/mbplanner_ws/src/sim/rotors_simulator/rotors_gazebo_plugins/src/external/gazebo_geotagged_images_plugin.cpp:25:16: fatal error: cv.h: 没有那个文件或目录

```
sudo gedit /home/zbxavier/mbplanner_ws/src/sim/rotors_simulator/rotors_gazebo_plugins/src/external/gazebo_geotagged_images_plugin.cpp
```

将文件中的`#include <opencv/cv.h>`替换为`#include <opencv2/opencv.hpp>`

---
/home/zbxavier/mbplanner_ws/src/sim/rotors_simulator/rotors_gazebo_plugins/src/external/gazebo_geotagged_images_plugin.cpp:26:21: fatal error: highgui.h: 没有那个文件或目录

```
sudo gedit /home/zbxavier/mbplanner_ws/src/sim/rotors_simulator/rotors_gazebo_plugins/src/external/gazebo_geotagged_images_plugin.cpp
```
```
#include <opencv2/highgui/highgui.hpp>
```
---

error: ‘CV_RGB2BGR’ was not declared in this scope

```
#include <opencv2/imgproc/types_c.h> 
```

---
CMake Error at /home/zbxavier/mbplanner_ws/devel/share/catkin_simple/cmake/catkin_simple-extras.cmake:38 (find_package):
  By not providing "Findimage_proc.cmake" in CMAKE_MODULE_PATH this project
  has asked CMake to find a package configuration file provided by
  "image_proc", but CMake did not find one.

  Could not find a package configuration file provided by "image_proc" with
  any of the following names:

    image_procConfig.cmake
    image_proc-config.cmake

  Add the installation prefix of "image_proc" to CMAKE_PREFIX_PATH or set
  "image_proc_DIR" to a directory containing one of the above files.  If
  "image_proc" provides a separate development package or SDK, be sure it has
  been installed.

```
git clone https://github.com/ros-perception/image_pipeline.git
git checkout noetic
```
复制到`mbplanner_ws/src`中一起编译

---

---