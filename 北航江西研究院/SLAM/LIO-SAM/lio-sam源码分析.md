# lio-sam源码

- imu校准分析

---

## imu校准分析

### class IMUPreintegration

- imuHandler(订阅imuTopic)，实时的IMU数据进来，修正后，转换得到雷达的姿态，发布里程计odomTopic+"_incremental"

- odometryHandler(订阅"lio_sam/mapping/odometry_incremental")，

### class TransformFusion

- lidarOdometryHandler(订阅"lio_sam/mapping/odometry")，

- imuOdometryHandler(订阅odomTopic+"_incremental")，


### class ImageProjection

- imuHandler(订阅imuTopic)，手动给出的的IMU转换，添加到 imuQueue

- odometryHandler(订阅odomTopic+"_incremental")，添加到 odomQueue

- cloudHandler(订阅pointCloudTopic)，调用imuDeskewInfo()和odomDeskewInfo()

### class FeatureExtraction

- laserCloudInfoHandler(订阅"lio_sam/deskew/cloud_info")

- publishFeatureCloud()，发布lio_sam/feature/cloud_info


### class mapOptimization

- laserCloudInfoHandler(订阅"lio_sam/feature/cloud_info")，调用publishOdometry

- loopInfoHandler(订阅"lio_loop/loop_closure_detection")

- publishOdometry()，发布"lio_sam/mapping/odometry",发布"lio_sam/mapping/odometry_incremental"

---