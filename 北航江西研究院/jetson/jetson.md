风扇
```
sudo /usr/bin/jetson_clocks
```

jtop系统监控
```
sudo -H pip install jetson-stats

jtop
```

查询工作模式
```
sudo nvpmodel -q verbose
```
修改工作模式
```
sudo nvpmodel -m 0
```