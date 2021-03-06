
　　OpenPose是一个实时多人系统，可以在单个图像上联合检测人体，手，面部和足部的关键点（总共135个关键点）。

##### 功能
- 二维实时多人关键点检测：
  - 15或18或25个关键点的身体/脚关键点估计。运行时间不依赖于检测到的人数。
  - 6点脚关键点估计。与25个关键点的身体/脚关键点检测器集成在一起。
  - 2x21-关键点的手关键点估计。目前，运行时间取决于在检测到人的数量。
  - 70个关键点面部关键点估计。目前，运行时间取决于在检测到人的数量。
- 3D实时单人关键点检测：
  - 从多个单一视图进行3D三角剖分。
  - 同步处理了Flir相机。
  - 与Flir / Point Grey相机兼容，但提供了C ++演示来添加您的自定义输入。
- 校准工具箱：
  - 容易估计失真，内部和外部相机参数。
  - 单人跟踪可进一步提高速度或视觉平滑度。

##### 输入
　　图像，视频，网络摄像头，Flir / Point Gray和IP摄像机。随附的C ++演示可添加您的自定义输入。

##### 输出
　　基本图像+关键点显示/保存（PNG，JPG，AVI等），关键点保存（JSON，XML，YML等）和/或关键点作为数组类。



---

```
source activate speech2gesture_env_py2-7

PYTHON_EXECUTABLE=/usr/bin/python2.7
PYTHON_LIBRARY=/usr/lib/x86_64-linux-gnu/libpython2.7m.so

sudo apt-get install python-dev
sudo pip3 install numpy opencv-python

```

```
source activate env_py3-7



sudo apt-get install python3-dev
sudo pip3 install numpy
sudo pip3 install opencv-python
```


```
cd /home/zb/OpenPoseFile/openpose/build/examples/tutorial_api_python

python3.7 01_body_from_image.py
```

```
ls ../../python/openpose
```

> pyopenpose.cpython-35m-x86_64-linux-gnu.so
pyopenpose.so


https://blog.csdn.net/dongkaiwen48/article/details/103150243

https://github.com/CMU-Perceptual-Computing-Lab/openpose/issues/1027


---
