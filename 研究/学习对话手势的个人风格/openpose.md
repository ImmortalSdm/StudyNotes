下载源码
```
git clone https://github.com/CMU-Perceptual-Computing-Lab/openpose.git
```

检查是否需要更新
```
git pull origin master
```

安装cmake-gui
```
sudo apt-get install cmake-qt-gui
```

下载模型
```
cd models
./getModels.sh
```

创建build文件
```
cd ..
mkdir build
```

---

## opencv
```
sudo apt update
sudo apt upgrade
sudo apt install libopencv-dev python-opencv

pkg-config --modversion opencv
```
---
## caffe
#### 依赖库
```
sudo apt-get --assume-yes install build-essential
sudo apt-get install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler
sudo apt-get install --no-install-recommends libboost-all-dev
#将遇到依赖问题
```

解决问题
```
sudo apt-get install aptitude

# n 会给出第二种解决方案
sudo aptitude install libboost-all-dev
```

```
sudo apt-get install --no-install-recommends libboost-all-dev
sudo apt-get install libopenblas-dev liblapack-dev libatlas-base-dev
sudo apt-get install libgflags-dev libgoogle-glog-dev liblmdb-dev

# Python libs
sudo apt install python-pip

sudo -H pip install --upgrade numpy protobuf

```
---

#### 正式安装caffe
```
git clone https://github.com/BVLC/caffe.git
```

用unzip命令解压
```
unzip caffe-master.zip
```

重命名为caffe
```
mv caffe-master caffe
```

切换到caffe所在的目录
```
cd caffe
```
---


首先将Makefile.config.example的内容复制到Makefile.config，因为make指令只能make Makefile.config文件，而Makefile.config.example是caffe给出的makefile例子
```
sudo cp Makefile.config.example Makefile.config
```

#### 修改配置文件Makefile.config：
```
sudo vim Makefile.config
```

- 应用 cudnn，将`#USE_CUDNN := 1`修改成`USE_CUDNN := 1`
- 应用 opencv 版本 如果opencv的版本是3。那么将#OPENCV_VERSION := 3 修改为：OPENCV_VERSION := 3
- 使用 python 接口，将`#WITH_PYTHON_LAYER := 1`修改为`WITH_PYTHON_LAYER := 1`
- `INCLUDE_DIRS:= $(PYTHON_INCLUDE) /usr/local/include`修改为`INCLUDE_DIRS:= $(PYTHON_INCLUDE) /usr/local/include /usr/include/hdf5/serial`
- `LIBRARY_DIRS:= $(PYTHON_LIB) /usr/local/lib /usr/lib`修改为`LIBRARY_DIRS:= $(PYTHON_LIB) /usr/local/lib /usr/lib /usr/lib/x86_64-linux-gnu/usr/lib/x86_64-linux-gnu/hdf5/serial`

#### 修改Makefile文件
```
sudo vim Makefile
```
- 将
`NVCCFLAGS +=-ccbin=$(CXX) -Xcompiler-fPIC$(COMMON_FLAGS)`
替换为
`NVCCFLAGS += -D_FORCE_INLINES -ccbin=$(CXX) -Xcompiler -fPIC $(COMMON_FLAGS)`
- 将`LIBRARIES += hdf5_hl hdf5`
改为`LIBRARIES += hdf5_serial_hl hdf5_serial`

#### host_config.h
```
sudo vim /usr/local/cuda/include/crt/host_config.h
```

将
```
#error-- unsupported GNU version! gcc versionslater than 6 are not supported!
```
改为
```
//#error-- unsupported GNU version! gcc versionslater than 6 are not supported!
```

#### 错误解决
```
sudo vim Makefile
```

- 添加`-std=c++11`至如下位置处：
![img](https://img-blog.csdnimg.cn/20191023165259670.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMDExMjc3,size_16,color_FFFFFF,t_70)

```
ll /usr/bin/gcc*

sudo ln -s /usr/bin/gcc-4.8 /usr/bin/gcc -f
sudo ln -s /usr/bin/gcc++-4.8 /usr/bin/gcc -f
sudo ln -s /usr/bin/g++-4.8 /usr/bin/gcc -f

sudo ln -s /usr/bin/gcc-4.8* /usr/bin/gcc -f
gcc --version

sudo ln -s /usr/bin/g++-4.8* /usr/bin/gcc -f
g++ --version

```

#### 编译

```
sudo make clean
sudo make all -j8
```



---
