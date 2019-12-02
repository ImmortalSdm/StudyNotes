##### 更新
```
sudo apt-get update
```

##### 删除
```
rm -R -v <文件/文件夹>
```

##### 复制
```
cp -R -v <源文件/文件夹> <目标文件/文件夹>
```

##### 权限更改
```
chmod -R -v 777 <文件/文件夹>
```

##### 解压tgz文件
```
tar   zxvf    <.tgz文件>  -C  <指定目录>
```

##### 清空回收站
```
cd ~/.local/share/Trash/

rm -rf files/*
```
还要从长计议

##### 查看显卡内存

```
watch -n 3 nvidia-smi
```
```
watch -n 3 nvidia-smi -a --display=utilization
```
##### 杀死进程

```
kill -9 <进程号PID>
```

##### 内存界面

```
top
```

##### deb

```
sudo dpkg -i <package.deb>
```
