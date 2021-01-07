https://content.xsens.com/download-mt-software-suite?submissionGuid=3389d0c2-f247-448a-9cb2-8f8a81c41cd7


https://www.xsens.com/hubfs/Downloads/Software/MTSS/Releases/2020.3.0-beta/MT_Software_Suite_linux-x64_2020.3.tar.gz?hsCtaTracking=71c605d6-e52c-41ae-994d-caf701dd10a5%7Cc589e17e-6073-4af9-b53e-a3609ac13e41

http://wiki.ros.org/xsens_mti_driver


https://base.xsens.com/hc/en-us/articles/360014235960-Interfacing-MTi-devices-with-the-NVIDIA-Jetson


---

安装ros驱动
```

```

安装sdk
```

```

xsens_ros_mti_driver
```
pushd src/xsens_ros_mti_driver/lib/xspublic && make && popd

catkin_make -j8


```
```
sudo chmod 777 /dev/ttyUSB0

roslaunch xsens_mti_driver display.launch
```