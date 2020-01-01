
#### atom

- `sudo dpkg -i`命令运行.deb安装文件
- `sudo apt-get -f install`
- `sudo apt-get update --fix-missing`
- 再`sudo dpkg -i`命令运行.deb安装文件

---


#### pycharm

- 解压到主目录
- 进入pycharm/bin
- `sudo sh ./pycharm.sh`

---

#### anaconda

- bash命令运行.sh的安装包

- Do you wish to proceed with the installation of Microsoft VSCode? [yes|no]”，输入no

- 切换到anaconda安装目录下运行 source bin/activate

- `conda init`

- `source ~/.bashrc`

---

#### git

```
sudo apt-get update

sudo apt-get upgrade

sudo apt install git

git config --global user.name "zb"

git config --global user.email "1037976812@qq.com"

```

---

#### 搜狗拼音

- `sudo dpkg -i`命令运行.deb安装文件
- `sudo apt-get -f install`
- `sudo apt-get update --fix-missing`
- 再`sudo dpkg -i`命令运行.deb安装文件

---

#### Chrome

```
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo dpkg -i google-chrome-stable_current_amd64.deb
```

---
#### vim

```
sudo apt-get install vim

```

---
#### cuda和cudnn


---

#### Google上网助手

---

#### gcc-5和g++-5

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

```
sudo mv gcc gcc.bak #备份
```
```
sudo ln -s gcc-5 gcc
```

再查看gcc版本号：
```
gcc -v
```


需要将g++链接改为g++-5：
```
sudo mv g++ g++.bak
```
```
sudo ln -s g++-5 g++
```
```
g++ -v
```
---
#### teamviewer
```
sudo dpkg -i '/home/zb/Downloads/teamviewer_15.1.3937_amd64.deb' 

sudo apt-get install -f

sudo dpkg -i '/home/zb/Downloads/teamviewer_15.1.3937_amd64.deb' 


sudo teamviewer daemon stop
sudo teamviewer daemon start
```

---




---




---
