
```
ulimit 限制 shell 以及从该 shell 内部启动的进程所占用的最大系统资源。大小通常以 Kbytes 为单位。

-d memory
限制分配给进程数据段的内存。

-f file.size
防止创建大于指定限制的文件。仅适用于 ext2 文件系统中的函数。

-s memory
限制栈空间。
```

# unalias abbreviation（取消别名）

`unalias` 删除现有的别名。当使用选项`-a`运行命令时，它会删除所有已知的别名。

# unset variable（取消变量）

`unset` 删除指定的变量。

```
until condition; do

commands

done
```

`until` 用于构建循环。循环一直执行，直到指定的条件满足。判断标准是作为条件的指定命令的返回值。比较和测试通过`test` 命令或其在方括号中的简写形式进行（见第 433 页）。

```
wait [process.number]
```

`wait` 等待指定的后台进程终止。当未指定进程编号时，命令会等待由 shell 启动的所有运行进程终止。

```
while condition; do

commands

done
```

`while` 用于构建循环。循环一直执行，直到指定的条件第一次不满足。判断标准是作为条件的指定命令的返回值。比较和测试通过`test` 命令或其在方括号中的简写形式进行（见第 433 页）。

# 13.7 特殊字符参考

在输入命令和编写 shell 程序时，都可以使用大量的特殊字符。下表总结了第四章（bash – 一种现代命令解释器）和本章涉及的所有特殊字符。

# BASH 编程

```
bash special characters
```
