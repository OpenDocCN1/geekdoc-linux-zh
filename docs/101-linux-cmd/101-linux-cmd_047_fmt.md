
# `yes`命令

Linux 中的`yes`命令用于打印给定`STRING`的连续输出流。如果未提供`STRING`，则打印“y”。它会重复输出字符串，直到被终止（例如使用`Ctrl + C`）。

## 示例

1. 在终端中无限期地打印“hello world”，直到被终止：

```sh
yes hello world
```

2. 一个更通用的命令：

```sh
yes [STRING]
```

## 选项

它接受以下选项：

1. `--help`

   > 显示此帮助信息并退出

2. `--version`

   > 输出版本信息并退出
