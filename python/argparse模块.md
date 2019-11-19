使用argparse模块编写命令行接口。

程序定义它需要的参数，然后argparse将弄清如何从sys.argv解析出那些参数。

argparse模块还会自动生成帮助和使用手册，并在用户给程序传入无效参数时报出错误信息。

- 1.创建解析器

```
parser = argparse.ArgumentParser(description='Process some integers.')
```

- 2.添加参数

```
parser.add_argument(
  '-output_path',
  '--output_path',
  type=str,
  default='/tmp'
  )
```

>name or flags - 一个命名或者一个选项字符串的列表，例如 foo 或 -f, --foo。
action - 当参数在命令行中出现时使用的动作基本类型。
nargs - 命令行参数应当消耗的数目。
const - 被一些 action 和 nargs 选择所需求的常数。
default - 当参数未在命令行中出现时使用的值。
type - 命令行参数应当被转换成的类型。
choices - 可用的参数的容器。
required - 此命令行选项是否可省略 （仅选项可用）。
help - 一个此选项作用的简单描述。
metavar - 在使用方法消息中使用的参数值示例。
dest - 被添加到 parse_args() 所返回对象上的属性名。

- 3.解析参数

```
>>> parser.parse_args(['--sum', '7', '-1', '42'])
Namespace(accumulate=<built-in function sum>, integers=[7, -1, 42])
```
