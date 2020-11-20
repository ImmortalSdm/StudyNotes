###### deb

```
sudo dpkg -i 
sudo apt-get -f install
sudo apt-get update --fix-missing
sudo dpkg -i
```

###### 切换cuda
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

###### tensorboard

```

```

```
source activate env_py3-7

tensorboard --logdir=/media/zb/411aa793-2c7b-9543-a172-1baa582a3d91/StylesOfConversationalGesture/tmp/audio_to_pose

tensorboard --logdir=/media/zb/411aa793-2c7b-9543-a172-1baa582a3d91/StylesOfConversationalGesture/tmp/stgcn_model
```


##### 增加交换空间

```
#查看
free -m

mkdir swap
cd swap 

#1024*20000000=20g
sudo dd if=/dev/zero of=swapfile bs=1024 count=30000000

#转换成 Swap 文件
sudo mkswap swapfile

#激活
sudo swapon swapfile

#再查看
free -m
```

卸载
```
#进入建立的 swap 文件目录。执行下列命令。 
sudo swapoff swapfile
```
如果需要一直保持这个 swap ，可以把它写入 /etc/fstab 文件。  

```
sudo vim /etc/fstab
home/lch/swap/swapfile none swap sw 0 0
```

##### 显卡问题

- 进入grub界面后
- advanced options for Ubuntu
- 再进入恢复模式
- 选择root Drop to root shell prompt回车
- 等一会，再次回车
- `mount -o remount /`
- `vi /etc/default/grub`
- "quiet splash"改为"quiet splash nomodeset"
- `:wq`保存
- `update-grub`更新
- ctrl+D
- 选择resume Resume normal boot

---

##### 更新
```
sudo apt-get update
```
---

##### 删除
```
rm -R -v <文件/文件夹>
```
---

##### 复制
```
cp -R -v <源文件/文件夹> <目标文件/文件夹>
```
---

##### 权限更改
```
chmod -R -v 777 <文件/文件夹>
```
---

##### 解压tgz文件
```
tar   zxvf    <.tgz文件>  -C  <指定目录>
```
---

##### 清空回收站
```
cd ~/.local/share/Trash/

rm -rf files/*
```

还要从长计议

---

##### 查看显卡内存

```
watch -n 1 nvidia-smi
```
```
watch -n 1 nvidia-smi -a --display=utilization
```
---

##### 杀死进程

```
kill -9 <进程号PID>
```
---

##### 内存界面

```
top
```
---

##### deb

```
sudo dpkg -i <package.deb>
```

---

##### 查找字符串
在命令模式下，输入/你要查找的字符

按下回车，可以看到vim把光标移动到该字符处

再按n（小写）查看下一个匹配

按N(大写）查看上一个匹配

---
##### 查看命令是否执行完毕

`echo $?` 命令，返回0，则说明上个执行命令已经成功执行
