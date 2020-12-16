# lio-sam源码

- imu校准分析

---

## imu校准分析

### class IMUPreintegration:
- imuHandler(订阅imuTopic)，实时的IMU数据进来，修正后，转换得到雷达的姿态，发布里程计"odometry/imu_incremental"
- odometryHandler(订阅"lio_sam/mapping/odometry_incremental")，

### class TransformFusion:
- lidarOdometryHandler(订阅"lio_sam/mapping/odometry")，
- imuOdometryHandler(订阅"odometry/imu_incremental")，


### class ImageProjection:
- imuHandler(订阅imuTopic)，手动给出的的IMU转换，添加到imuQueue
- odometryHandler(订阅"odometry/imu_incremental")，添加到odomQueue
- cloudHandler(订阅pointCloudTopic)，


### mapOptimization:
- laserCloudInfoHandler(订阅"lio_sam/feature/cloud_info")，调用publishOdometry
- gpsHandler(订阅gpsTopic)
- loopInfoHandler(订阅"lio_loop/loop_closure_detection")
- publishOdometry()，发布"lio_sam/mapping/odometry",发布"lio_sam/mapping/odometry_incremental"

---