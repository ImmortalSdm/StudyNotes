# IMU标定

- lio-sam中使用IMU的方法分析
- 使用lidar_align校准小车所使用ZED2中的IMU


---

## 一、lio-sam中使用IMU的方法分析

![](lio-sam代码结构.png)

在lio-sam中，实时的IMU数据首先用extrinsicRPY和extrinsicRot进行转换，转换后再与prevStateOdom和prevBiasOdom一起计算得到imuPose，最后通过给出的extrinsicTrans计算出lidarPose。

每一次采集雷达数据都会使用gtsam的概率图模型的优化器来对prevStateOdom和prevBiasOdom进行修正（也就是对原始IMU数据进行修正）。

因此LIO-SAM本身的里程计就较为准确，在不纠正IMU的情况下也不会发生里程计较大的偏移。

外参设置：
- extrinsicRPY和extrinsicRot是作为imu本身的偏转进行纠正。
- extrinsicTrans是用来计算lidar与imu之间的坐标转换



---


## 二、使用lidar_align校准小车所使用ZED2中的IMU

lidar_align是一种激光雷达与IMU之间外参校准的方法。

若校准正确，则按照imu数据模拟的里程计发布的点云会更清晰。

https://github.com/ethz-asl/lidar_align

- 采集小车上ZED2的IMU以及雷达数据
- 将采集的数据使用lidar_align进行拟合（没有lidar_align需要用到的geometry_msgs/TransformStamped类型数据，需要将代码改为sensor_msgs/Imu数据格式）
- 使用lidar_align得到的结果修正lio-sam所使用的imu数据


经过几十分钟的拟合后，得到了lidar_align求出的修正值：

平移extrinsicTrans
[-0.0100746,0.000484179,0.0395583]

角度的四元数
[0.567411,-0.0726565,0.0934026,0.814887]

- 校准质量与观察到的所进行的运动密切相关，小车几乎没有垂直运动，将导致该方向上的估计错误。
- lidar_align只能对短时间（小几十秒）的数据进行校准，若时间太长，则拟合校准数据超过几个G，所需运行内存超过几十个G，在xavier上将无法校准，这导致数据采集不完善

IMU外参拟合结果并不理想，不适用于小车，若需要校准，必须再找别的方式。


---