# lio-sam中的IMU标定总结

- lio-sam中使用IMU的方法分析
- lidar_align分析
- 使用lidar_align校准小车所使用ZED2中的IMU
- 实验结果

---

## 一、lio-sam中使用IMU的方法分析

![](lio-sam代码结构.png)

在lio-sam中，实时的IMU数据将与prevStateOdom和prevBiasOdom一起计算得到imuPose，然后再通过给出的extrinsicTrans计算出lidarPose。

而prevStateOdom和prevBiasOdom是使用gtsam的概率图模型来进行计算的，每一次采集雷达数据都会对prevStateOdom和prevBiasOdom进行修正。


---

## 二、lidar_align分析

lidar_align是一种激光雷达与IMU之间外部校准的方法。

https://github.com/ethz-asl/lidar_align



---

## 三、使用lidar_align校准小车所使用ZED2中的IMU

---

## 四、实验结果