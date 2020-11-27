
## 简单的c++节点

```
#include <ros/ros.h>

int main(int argc,char **argv){

    ros::init(argc,argv,"minimal");
    ros::NodeHandle n;
    ros::spin();

    return 0;
}
```