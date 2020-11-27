## 简单的c++节点

myNode.cpp
```
//c++编写ROS节点必须包含ros.h头文件
#include <ros/ros.h>

int main(int argc,char **argv){

    //节点初始化，并命名
    ros::init(argc,argv,"minimal");
    
    //创建一个节点句柄，用来创建话题、服务和动作
    ros::NodeHandle n;

    //等待ROS调度
    ros::spin();

    return 0;
}
```
在CMakeList.txt和package.xml中指定依赖库

CMakeList.txt
```
cmake_minimum_required(VERSION 2.8.3)
project(first_cpp)#项目名

find_package(catkin REQUIRED roscpp)

#编译文件
add_executable(myNode src/myNode.cpp)
#依赖库
target_link_libraries(myNode
    ${catkin_LIBRARIES}
)
```

package.xml
```

```