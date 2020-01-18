```
apt-get update
```

```
apt-get upgrade
```

安装：
```
sudo apt install git
```

配置姓名：
```
git config --global user.name "zb"
```

配置邮箱：
```
git config --global user.email "1037976812@qq.com"
```

查看配置结果
```
git config --list
```

查看更多git命令
```
git --help
```

---

### 配置GitHub公钥

```
cd ~/.ssh
```
如果没有就'mkdir ~/.ssh'
```
git config --global user.name "MonsterMoriarty"
git config --global user.email "www.1037976812@qq.com"
```
```
ssh-keygen -t rsa -C "www.1037976812@qq.com"
```
```
ls
cat id_rsa.pub
#cat命令查看文件内容，就不用进入文件编辑了
```
复制公钥到GitHub中设置ssh

测试连接
```
ssh git@github.com
```



---
