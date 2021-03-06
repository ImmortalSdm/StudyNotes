```
sudo apt-get install ffmpeg
```

##### 创建anaconda环境
```
conda create --name env_py2-7 python=2.7 anaconda

conda create --name env_py3-7 python=3.7 anaconda

conda create --name env_py3-6 python=3.6 anaconda

# Music-oriented Dance Video Synthesis with Pose Perceptual Loss
conda create --name env_py3-5_MODVS python=3.5 anaconda

# 虚拟机
conda create --name env_py2-7 python=2.7 anaconda
```


##### 激活anaconda环境
```
source activate env_py2-7
source activate env_py3-7
source activate env_py3-6
source activate env_py3-5_MODVS
```

```
pip install tensorflow_gpu-1.9.0-cp27-cp27mu-manylinux1_x86_64.whl

pip install -i https://pypi.tuna.tsinghua.edu.cn/simple tensorflow-gpu==1.13.1
```

```
pip install -r requirments.txt

#或者用conda

conda install pandas==0.24.2
pip install tqdm==4.32.2
```

cv2：
```
conda install opencv



```

youtube-dl：
```
sudo apt-get install youtube-dl
```

---

### 1. 下载cuda及其补丁
[cuda_9.0.176_384.81_linux.run](https://developer.download.nvidia.com/compute/cuda/9.0/secure/Prod/local_installers/cuda_9.0.176_384.81_linux.run?j_S72UF5E3JBxLRAxClXK4uwOoFaKo-qZKgtLzn9hvE8217Fh9nE_efls2oQHDQDSPqTS7eMdweECSnO2Aaebbwt9ManGjkarcOuFsu5rSWyTFH3-4mJJf1guYdvhtu1ogYqE40uLIZv2i1OFf2huDmwQZ71XTBgk3jqwf4hgBMOoLeTHI86t4DE)

### 2. 下载cudnn7.6.2

### 3. 安装cuda

##### 3.1. GCC 降级

由于CUDA 9.0仅支持GCC 6.0及以下版本，而Ubuntu 19.10预装GCC版本为9.0，故手动进行降级：

修改源
```
sudo gedit /etc/apt/sources.list
```

在打开的文件中最后面加上这两行
```
deb http://dk.archive.ubuntu.com/ubuntu/ xenial main
deb http://dk.archive.ubuntu.com/ubuntu/ xenial universe
```

更新源
```
sudo apt update
```

安装
```
sudo apt-get install gcc-5
```
```
sudo apt-get install g++-5
```

装完后进入到/usr/bin目录下

```
cd /usr/bin
ls -l gcc*
```
会显示以下结果
> lrwxrwxrwx 1 root root 7th May 16 18:16 /usr/bin/gcc -> gcc-9.0


发现gcc链接到gcc-9.0, 需要将它改为链接到gcc-5，方法如下:
```
sudo mv gcc gcc.bak #备份
```
```
sudo ln -s gcc-5 gcc #重新链接
```

再查看gcc版本号：
```
gcc -v
```

同理，对g++也做同样的修改：
```
ls -l g++*
```
> lrwxrwxrwx 1 root root 7th May 15:17 g++ -> g++-7.3


需要将g++链接改为g++ -5：
```
sudo mv g++ g++.bak
```
```
sudo ln -s g++-5 g++
```

查看g++版本号：
```
g++ -v
```


##### 3.2. 安装cuda 及其补丁

```
sudo sh cuda_9.0.176_384.81_linux.run
```

之前已经安装过显卡驱动程序，故在提问是否安装显卡驱动时选择no

其他选择默认路径或者yes即可。

然后，继续执行以下操作安装4个 patch ：
```
sudo sh cuda_9.0.176.1_linux.run
```
```
sudo sh cuda_9.0.176.2_linux.run
```
```
sudo sh cuda_9.0.176.3_linux.run
```
```
sudo sh cuda_9.0.176.4_linux.run
```

将以下两条加入.bashrc文件中
```
sudo vim ~/.bashrc
```

```
export PATH=/usr/local/cuda/bin${PATH:+:$PATH}
export LD_LIBRARY_PATH=/usr/local/cuda/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
```
```
source ~/.bashrc
```

## 切换cuda
```
cd /usr/local
sudo rm -R -v cuda

# cycleGAN
sudo ln -s /usr/local/cuda-8.0 /usr/local/cuda

# StylesOfConversationalGesture
sudo ln -s /usr/local/cuda-9.0 /usr/local/cuda

# openpose/caffe
sudo ln -s /usr/local/cuda-10.0 /usr/local/cuda

```

---

#### cuda8.0 比较特殊

- 直接安装若报错——安装不了tool

```
sh cuda_8.0.61_375.26_linux.run --tar mxvf

sudo cp -R -v InstallUtils.pm /usr/lib/x86_64-linux-gnu/perl-base

export $PERL5LIB
```

- 再安装报错——确认路径问题，则
```
sudo gedit /etc/profile 
# 加入export PATH=/usr/local/cuda/bin${PATH:+:$PATH}
```
```
sudo gedit /etc/ld.so.conf.d/cuda.conf # 加入/usr/local/cuda/lib64
```
```
sudo ldconfig
```

- 打补丁

- 测试
```
cd /usr/local/cuda-8.0/samples/1_Utilities/deviceQuery  
make -j4  
sudo ./deviceQuery  
```

---

### 4. 安装cuDNN

##### 4.1 解压cuDNN

##### 4.2 复制cuDNN内容到cuda相关文件夹内：
```
cd cudnn-9.0-linux-x64-v7.6.2.24
```
```
sudo cp cuda/include/cudnn.h    /usr/local/cuda-8.0/include
sudo cp cuda/include/cudnn.h    /usr/local/cuda-9.0/include
sudo cp cuda/include/cudnn.h    /usr/local/cuda-10.0/include
```
```
sudo cp cuda/lib64/libcudnn*    /usr/local/cuda-8.0/lib64
sudo cp cuda/lib64/libcudnn*    /usr/local/cuda-9.0/lib64
sudo cp cuda/lib64/libcudnn*    /usr/local/cuda-10.0/lib64
```
```
sudo chmod a+r /usr/local/cuda/include/cudnn.h  /usr/local/cuda-8.0/lib64/libcudnn*
sudo chmod a+r /usr/local/cuda/include/cudnn.h  /usr/local/cuda-9.0/lib64/libcudnn*
sudo chmod a+r /usr/local/cuda/include/cudnn.h  /usr/local/cuda-10.0/lib64/libcudnn*
```
---


[下载tensorflow-gpu py3-7](https://files.pythonhosted.org/packages/a1/eb/bc0784af18f612838f90419cf4805c37c20ddb957f5ffe0c42144562dcfa/tensorflow_gpu-2.0.0-cp37-cp37m-manylinux2010_x86_64.whl)

[下载tensorflow-gpu py2-7](https://files.pythonhosted.org/packages/68/45/8ed49fb2decd4ce7849fc9755d9e066f414fb29c40e811bf4c12287de0af/tensorflow_gpu-1.9.0-cp27-cp27mu-manylinux1_x86_64.whl)

---
## 提取数据

extract
```
python -m data.train_test_data_extraction.extract_data_for_training --base_dataset_path ../ --speaker oliver
```


---
## 激活anaconda环境
```
source activate env_py2-7
```

## 训练
```
python -m audio_to_multiple_pose_gan.train --gans 1 --name test_run --arch_g audio_to_pose_gans --arch_d D_patchgan --speaker oliver --output_path ../tmp --train_csv ../train.csv --batch_size 32
```

---




？？？

出大事！

cuda:
```
wget http://developer.download.nvidia.com/compute/cuda/10.1/Prod/local_installers/cuda_10.1.243_418.87.00_linux.run
```
```
sudo sh cuda_10.1.243_418.87.00_linux.run
```
