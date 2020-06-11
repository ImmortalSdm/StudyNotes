
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

- bash命令运行.sh的安装包(复制到home目录，才会安装在这里)

- Do you wish to proceed with the installation of Microsoft VSCode? [yes|no]”，输入no

- 切换到anaconda安装目录下运行 source bin/activate
```
source bin/activate
conda init
source ~/.bashrc
conda  --version
```

```

source activate env_py2-7


```

```
conda config --add channels 'https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main'

conda config --add channels 'https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free'

conda config --add channels 'https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r'

conda config --add channels 'https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/pro'

conda config --add channels 'https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/msys2'

conda config --set show_channel_urls yes

conda clean -i
```

---

#### git

```
sudo apt-get update

sudo apt-get upgrade

sudo apt install git

git config --global user.name "MonsterNoriarty"

git config --global user.email "www.1037976812@qq.com"

git config --global credential.helper store #记住密码
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


解压文件
```
cd /home/zb/Downloads/Ghelper_1.4.6.beta
```
Chrome浏览器中，添加已解压扩展程序ghelper_source

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
cd /usr/bin
```
```
sudo mv gcc gcc.bak
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


sudo teamviewer --daemon enable
sudo systemctl start teamviewerd.service

sudo teamviewer daemon stop
sudo teamviewer daemon start


```

---

#### pip

```
sudo apt update


sudo apt install python-pip
```

---




---
