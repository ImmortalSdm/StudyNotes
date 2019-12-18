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

正式安装caffe
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

修改Makefile.config




















---
