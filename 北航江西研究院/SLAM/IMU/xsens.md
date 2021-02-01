# xsens 安装配置记录


## 安装ros驱动
```
sudo apt-get install ros-melodic-xsens-driver
```

## 下载软件包
```
链接：https://pan.baidu.com/s/1NtMoWnVu2NhpfZzoKpHYIA 
提取码：bhjx 
```


## 安装sdk（文件在软件包中）
```
sudo ./mtsdk_linux-x64_2020.3.sh
```

## 在windows上安装MT manager（文件在软件包中，仅配置时需要）

配置如下：
![](xsens配置.png)
- 旋转角必须设置为四元数，不可使用欧拉角
- 惯性数据输出为Rate of Turn 以及 Accelerate（带重力加速度）

- Zed2的频率为300hz，因此频率设置为400hz



![](xsens配置2.png)

其中，UART接口的波特率与传输数据的频率有关，波特率太低会导致丢失数据，在双400hz的频率下，460800的波特率是可以正常工作的。

滤波设置使用场景及介绍如下：

![](xsens配置滤波.png)
![](xsens配置滤波2.png)
![](xsens配置滤波3.png)

## 安装ros驱动

- 从/usr/local/xsens/xsens_ros_mti_driver复制到ros的工作空间

- xsens_ros_mti_driver
```
pushd src/xsens_ros_mti_driver/lib/xspublic && make && popd

catkin_make -j8
```

## 运行demo

setserial设置低延时模式保证帧率稳定
```
sudo apt-get install setserial
```

```
sudo chmod 777 /dev/ttyUSB*
setserial /dev/ttyUSB0 low_latency
roslaunch xsens_mti_driver display.launch
```

此时已经可以读取到/imu/data数据

---

https://content.xsens.com/download-mt-software-suite?submissionGuid=3389d0c2-f247-448a-9cb2-8f8a81c41cd7


https://www.xsens.com/hubfs/Downloads/Software/MTSS/Releases/2020.3.0-beta/MT_Software_Suite_linux-x64_2020.3.tar.gz?hsCtaTracking=71c605d6-e52c-41ae-994d-caf701dd10a5%7Cc589e17e-6073-4af9-b53e-a3609ac13e41

http://wiki.ros.org/xsens_mti_driver


https://base.xsens.com/hc/en-us/articles/360014235960-Interfacing-MTi-devices-with-the-NVIDIA-Jetson

---