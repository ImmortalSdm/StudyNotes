# lio-sam中的IMU标定总结

- lio-sam中使用IMU的方法分析
- lidar_align分析
- 使用lidar_align校准小车所使用ZED2中的IMU
- 实验结果

---

## 一、lio-sam中使用IMU的方法分析

![](lio-sam代码结构.png)

在lio-sam中，实时的IMU数据首先用extrinsicRPY和extrinsicRot进行转换，转换后再与prevStateOdom和prevBiasOdom一起计算得到imuPose，然后通过给出的extrinsicTrans计算出lidarPose。

每一次采集雷达数据都会使用gtsam的概率图模型的优化器来对prevStateOdom和prevBiasOdom进行修正。

外参设置：
- extrinsicRPY和extrinsicRot是作为imu本身的偏转进行纠正。
- extrinsicTrans是用来计算lidar与imu之间的坐标转换

---

## 二、lidar_align分析

lidar_align是一种激光雷达与IMU之间外参校准的方法。

https://github.com/ethz-asl/lidar_align

校准质量与观察到的所进行的运动密切相关，而小车几乎没有垂直运动，将导致该方向上的估计错误。

---

## 三、使用lidar_align校准小车所使用ZED2中的IMU

- 采集小车上ZED2的IMU以及雷达数据
 - 将采集的数据使用lidar_align进行拟合（没有lidar_align需要用到的geometry_msgs/TransformStamped类型数据，需要将代码改为sensor_msgs/Imu数据格式）
 - 使用lidar_align得到的结果修正lio-sam所使用的imu数据

---

## 四、实验结果

经过几十分钟的拟合后，得到了lidar_align求出的修正值：

