
`python xxx.py`直接运行，把py文件，所在的目录放到了sys.path属性中，将会调用`if __name__ == "__main__":`中的代码。

`python -m`将库中的python模块用作脚本去运行，相当于import，模块启动，把你输入命令的目录（也就是当前路径），放到了sys.path属性中，将不会调用`if __name__ == "__main__":`的代码。

---



























---
