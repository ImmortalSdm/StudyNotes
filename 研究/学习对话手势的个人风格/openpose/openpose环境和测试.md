## opencv
```
sudo apt update
sudo apt upgrade
sudo apt install libopencv-dev python-opencv

pkg-config --modversion opencv

```

## caffe
#### 依赖库
https://blog.csdn.net/weixin_39059031/article/details/84823717
https://blog.csdn.net/weixin_39059031/article/details/84824659
```
sudo apt-get install libatlas-base-dev
sudo apt-get install libgoogle-glog-dev
sudo apt-get install -y build-essential cmake git pkg-config
sudo apt-get install -y libprotobuf-dev libleveldb-dev libsnappy-dev libhdf5-serial-dev protobuf-compiler
sudo apt-get install -y --no-install-recommends libboost-all-dev
sudo apt-get install -y libgflags-dev libgoogle-glog-dev liblmdb-dev
```

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

```
sudo apt-get install python-numpy python-scipy python-matplotlib ipython python-pandas python-sympy
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
cd /home/zb/OpenPoseFile/caffe
cp Makefile.config.example Makefile.config
sudo gedit Makefile.config
```

- 应用 cudnn，将`#USE_CUDNN := 1`修改成`USE_CUDNN := 1`

- 应用 opencv 版本 如果opencv的版本是3。那么将#OPENCV_VERSION := 3 修改为：OPENCV_VERSION := 3

- 使用 python 接口，将`#WITH_PYTHON_LAYER := 1`修改为`WITH_PYTHON_LAYER := 1`

- `INCLUDE_DIRS:= $(PYTHON_INCLUDE) /usr/local/include`修改为`INCLUDE_DIRS:= $(PYTHON_INCLUDE) /usr/local/include /usr/include/hdf5/serial`

- `LIBRARY_DIRS:= $(PYTHON_LIB) /usr/local/lib /usr/lib`修改为`LIBRARY_DIRS:= $(PYTHON_LIB) /usr/local/lib /usr/lib /usr/lib/x86_64-linux-gnu/usr/lib/x86_64-linux-gnu/hdf5/serial`

- compute那一部分改一改

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

- `LIBRARIES += boost_thread stdc++`改为`LIBRARIES += boost_thread stdc++ boost_regex`

- 编辑/usr/local/cuda/include/host_config.h，将其中的第115行注释，如下
```
//#error-- unsupported GNU version! gcc versions later than 4.9 are not supported!
```

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
---
### 错误解决

##### 编译安装protobuf
```
sudo apt-get autoremove libprotobuf-dev protobuf-compiler
sudo apt-get remove libprotobuf-dev
sudo apt-get remove libprotobuf-compile
sudo apt-get remove protobuf-compiler
```
```
cd protobuf
sudo apt-get install libtool
./autogen.sh
./configure --prefix=/usr/local/ CC=/usr/bin/gcc
sudo make clean
sudo make -j8

sudo make install

```
```
cd /etc/ld.so.conf.d
sudo touch libprotobuf.conf
sudo vim libprotobuf.conf # 加入/usr/local/lib
sudo ldconfig
protoc --version
```
##### 2

```
sudo vim Makefile
```

- 添加`-std=c++11`至如下位置处：
![img](https://img-blog.csdnimg.cn/20191023165259670.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMDExMjc3,size_16,color_FFFFFF,t_70)

---

报错
```
/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `leveldb::Status::ToString() const'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `google::protobuf::internal::WireFormatLite::WriteString(int, std::string const&, google::protobuf::io::CodedOutputStream*)'
collect2: error: ld returned 1 exit status
make: *** [Makefile:643：.build_release/examples/siamese/convert_mnist_siamese_data.bin] 错误 1
```

##### gcc


```
sudo ln -s /usr/bin/gcc-4.8* /usr/bin/gcc -f
sudo ln -s /usr/bin/gcc-ar-4.8* /usr/bin/gcc-ar -f
sudo ln -s /usr/bin/gcc-4.8* /usr/bin/gcc.bak -f
sudo ln -s /usr/bin/gcc-nm-4.8* /usr/bin/gcc-nm -f
sudo ln -s /usr/bin/gcc-ranlib-4.8* /usr/bin/gcc-ranlib -f
sudo ln -s /usr/bin/g++-4.8* /usr/bin/g++ -f
sudo ln -s /usr/bin/g++-4.8* /usr/bin/g++.bak -f
```

```
sudo ln -s /usr/bin/x86_64-linux-gnu-gcc-9* /usr/bin/gcc -f
sudo ln -s /usr/bin/x86_64-linux-gnu-gcc-ar-9* /usr/bin/gcc-ar -f
sudo ln -s /usr/bin/x86_64-linux-gnu-gcc-9* /usr/bin/gcc.bak -f
sudo ln -s /usr/bin/x86_64-linux-gnu-gcc-nm-9* /usr/bin/gcc-nm -f
sudo ln -s /usr/bin/x86_64-linux-gnu-gcc-ranlib-9* /usr/bin/gcc-ranlib -f
sudo ln -s /usr/bin/x86_64-linux-gnu-g++-9* /usr/bin/g++ -f
sudo ln -s /usr/bin/x86_64-linux-gnu-g++-9* /usr/bin/g++.bak -f
```
```
sudo ln -s /usr/bin/gcc-4.8* /usr/bin/gcc -f
sudo ln -s /usr/bin/g++-4.8* /usr/bin/g++ -f
```
```
sudo ln -s /usr/bin/x86_64-linux-gnu-gcc-9* /usr/bin/gcc -f
sudo ln -s /usr/bin/x86_64-linux-gnu-g++-9* /usr/bin/g++ -f
```

```
ll /usr/bin/gcc*
ll /usr/bin/g++*
```
##### remove the gcc  error from the CUDA header

```
sudo vim /usr/local/cuda/include/crt/host_config.h
```

```
//#if __GNUC__ > 6

/*#error -- unsupported GNU version! gcc versions later than 6 are not suppo    rted! */

//#endif
/* __GNUC__ > 6 */
```

---



#### 编译caffe

layer_clip的问题要改



```
sudo make clean
sudo make all -j`nproc`
sudo make test -j`nproc`
make runtest -j`nproc`
```



##### 报错，暂未解决？


```
F1231 15:26:33.385639  6133 cudnn_softmax_layer.cu:20] Check failed: status == CUDNN_STATUS_SUCCESS (8 vs. 0)  CUDNN_STATUS_EXECUTION_FAILED
```


禁用cudnn可以运行，但速度慢


##### 报错

```
src/caffe/util/io.cpp: In function ‘bool caffe::ReadProtoFromBinaryFile(const char*, google::protobuf::Message*)’:
src/caffe/util/io.cpp:57:66: warning: ‘void google::protobuf::io::CodedInputStream::SetTotalBytesLimit(int, int)’ is deprecated (declared at /usr/local/include/google/protobuf/io/coded_stream.h:397): Please use the single parameter version of SetTotalBytesLimit(). The second parameter is ignored. [-Wdeprecated-declarations]
   coded_input->SetTotalBytesLimit(kProtoReadBytesLimit, 536870912);
                                                                  ^
AR -o .build_release/lib/libcaffe.a
LD -o .build_release/lib/libcaffe.so.1.0.0
CXX/LD -o .build_release/tools/compute_image_mean.bin
CXX/LD -o .build_release/tools/upgrade_solver_proto_text.bin
CXX/LD -o .build_release/tools/upgrade_net_proto_binary.bin
CXX/LD -o .build_release/tools/extract_features.bin
CXX/LD -o .build_release/tools/convert_imageset.bin
CXX/LD -o .build_release/tools/caffe.bin
CXX/LD -o .build_release/tools/upgrade_net_proto_text.bisrc/caffe/util/io.cpp:57:66: warning: ‘void google::protobuf::io::CodedInputStream::SetTotalBytesLimit(int, int)’ is deprecated (declared at /usr/local/include/google/protobuf/io/coded_stream.h:397): Please use the single parameter version of SetTotalBytesLimit(). The second parameter is ignored. [-Wdeprecated-declarations]
   coded_input->SetTotalBytesLimit(kProtoReadBytesLimit, 536870912);

convert_mnist_data.cpp:(.text.startup+0x114): undefined reference to `google::SetUsageMessage(std::string const&)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `leveldb::DB::Open(leveldb::Options const&, std::string const&, leveldb::DB**)'
/usr/bin/ld: .build_release/lib/libcaffe.so: undefined reference to `leveldb::Status::ToString() const'
collect2: error: ld returned 1 exit status
make: *** [Makefile:643：.build_release/examples/mnist/convert_mnist_data.bin] 错误 1

```
尝试解决
```
sudo apt-get install gcc-5
sudo apt-get install g++-5

cd /usr/bin

sudo mv gcc gcc48.bak
sudo mv g++ g++48.bak

sudo ln -s gcc-5 gcc
sudo ln -s g++-5 g++
```
然后重新编译protobuf。

然后再试试编译caffe
```
sudo make clean
sudo make all -j`nproc`
sudo make test -j`nproc`
make runtest -j`nproc`
# 不可用sudo，cuda环境配置在用户目录下，但是我们sudo runtest 是用的root用户
```
成功!

```
export LD_LIBRARY_PATH=/home/zb/OpenPoseFile/caffe/.build_release/:$LD_LIBRARY_PATH
```


---

## 正式openpose

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

打开
```
cmake-gui
```

```
cd /home/zb/OpenPoseFile/caffe
sudo protoc src/caffe/proto/caffe.proto --cpp_out=.
sudo mkdir include/caffe/proto
sudo mv src/caffe/proto/caffe.pb.h include/caffe/proto
```

```
cd /home/zb/OpenPoseFile/openpose/build

make clean

make -j`nproc`
```

报错
```
nvcc fatal   : Unsupported gpu architecture 'compute_75'
```

在openpose / cmake / Cuda.cmake 中注释以下行（APPEND CUDA_NVCC_FLAGS $ {NVCC_FLAGS_EXTRA}）



```
cd /home/zb/OpenPoseFile/openpose/build

make clean

make -j`nproc`
```
成功

---

运行

```
./build/examples/openpose/openpose.bin --video examples/media/video.avi
```

```
[libprotobuf ERROR google/protobuf/message_lite.cc:123] Can't parse message of type "caffe.NetParameter" because it is missing required fields: layer[0].clip_param.min, layer[0].clip_param.max
F1219 17:32:23.850667 32687 upgrade_proto.cpp:97] Check failed: ReadProtoFromBinaryFile(param_file, param) Failed to parse NetParameter file: models/pose/body_25/pose_iter_584000.caffemodel
已放弃 (核心已转储)
```
https://github.com/CMU-Perceptual-Computing-Lab/openpose/issues/787

https://github.com/BVLC/caffe/commit/dc6d3303a45e8c5a0fe7249881ca6bd8387c9203

恢复后报错

```
F1219 20:05:53.700925 20373 cudnn_conv_layer.cu:28] Check failed: status == CUDNN_STATUS_SUCCESS (8 vs. 0)  CUDNN_STATUS_EXECUTION_FAILED
已放弃 (核心已转储)
```



---
