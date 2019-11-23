```
sudo apt-get install ffmpeg
```

create
```
conda create --name speech2gesture_env_py27 python=2.7 anaconda
```


start
```
source activate speech2gesture_env_py27
```

```
pip install tensorflow_gpu-1.9.0-cp27-cp27mu-manylinux1_x86_64.whl
```

```
pip install -r requirments.txt
```

---

### 1. 下载cuda及其补丁
[cuda_9.0.176_384.81_linux.run](https://developer.download.nvidia.com/compute/cuda/9.0/secure/Prod/local_installers/cuda_9.0.176_384.81_linux.run?j_S72UF5E3JBxLRAxClXK4uwOoFaKo-qZKgtLzn9hvE8217Fh9nE_efls2oQHDQDSPqTS7eMdweECSnO2Aaebbwt9ManGjkarcOuFsu5rSWyTFH3-4mJJf1guYdvhtu1ogYqE40uLIZv2i1OFf2huDmwQZ71XTBgk3jqwf4hgBMOoLeTHI86t4DE)

### 2. 下载cudnn7.6.2

### 3. 安装cuda

##### 3.1. GCC 降级

由于CUDA 9.0仅支持GCC 6.0及以下版本，而Ubuntu 19.10预装GCC版本为9.0，故手动进行降级：
```
sudo apt-get install gcc-4.8
```
```
sudo apt-get install g++-4.8
```

装完后进入到/usr/bin目录下
```
ls -l gcc*
```
会显示以下结果
> lrwxrwxrwx 1 root root 7th May 16 18:16 /usr/bin/gcc -> gcc-9.0


发现gcc链接到gcc-9.0, 需要将它改为链接到gcc-4.8，方法如下:
```
sudo mv gcc gcc.bak #备份
```
```
sudo ln -s gcc-4.8 gcc #重新链接
```

同理，对g++也做同样的修改：
```
ls -l g++*
```
> lrwxrwxrwx 1 root root 7th May 15:17 g++ -> g++-7.3


需要将g++链接改为g++-4.8:
```
sudo mv g++ g++.bak
```
```
sudo ln -s g++-4.8 g++
```

再查看gcc和g++版本号：
```
gcc -v g++ -v
```
均显示gcc version 4.8 ，说明gcc 4.8安装成功。

##### 3.2. 安装cuda 及其补丁

---

extract
```
python -m data.train_test_data_extraction.extract_data_for_training --base_dataset_path ../ --speaker oliver
```



训练
```
python -m audio_to_multiple_pose_gan.train --gans 1 --name test_run --arch_g audio_to_pose_gans --arch_d pose_D --speaker oliver --output_path ../tmp
```

预测
```
python -m audio_to_multiple_pose_gan.predict_to_videos --train_csv ../train.csv --seq_len 64 --output_path ../tmp/my_output_folder --speaker oliver -ag audio_to_pose_gans --gans 1
```

---


[tensorflow-gpu py37](https://files.pythonhosted.org/packages/a1/eb/bc0784af18f612838f90419cf4805c37c20ddb957f5ffe0c42144562dcfa/tensorflow_gpu-2.0.0-cp37-cp37m-manylinux2010_x86_64.whl)

[tensorflow-gpu py27](https://files.pythonhosted.org/packages/68/45/8ed49fb2decd4ce7849fc9755d9e066f414fb29c40e811bf4c12287de0af/tensorflow_gpu-1.9.0-cp27-cp27mu-manylinux1_x86_64.whl)

---

cuda:
```
wget http://developer.download.nvidia.com/compute/cuda/10.1/Prod/local_installers/cuda_10.1.243_418.87.00_linux.run
```
```
sudo sh cuda_10.1.243_418.87.00_linux.run
```
