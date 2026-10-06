
`printf` 命令允许我们格式化两个变量的输出，在这种情况下使用科学计数法显示阶乘值：

```
$ ./test4
The factorial of 1 is 1.00e+00
The factorial of 2 is 2.00e+00
The factorial of 3 is 6.00e+00
The factorial of 4 is 2.40e+01
The factorial of 5 is 1.20e+02
The factorial of 6 is 7.20e+02
The factorial of 7 is 5.04e+03
The factorial of 8 is 4.03e+04
The factorial of 9 is 3.63e+05
The factorial of 10 is 3.63e+06
```

 `%6.2e` 格式指定了一个六位的科学计数法值，小数点后保留两位。

## ulimit 命令

`ulimit` 命令是 dash shell 的一个极佳补充。它允许你限制系统资源，以防止 shell 中过度使用。你设置的限制适用于运行 `ulimit` 命令的该 shell。

在 dash shell 中，你可以使用两种类型的限制：

- 硬限制（hard limit），只能由 root 用户账户重置。
- 软限制（soft limit），可以由该 shell 的所有者账户重置。

当 shell 违反硬限制时，会发生错误并阻塞操作。这是一个防止系统过载的绝佳工具。

`ulimit` 命令使用几个命令行参数来定义系统资源限制。这些参数在表 20-6 中。

## 第四部分 替代 Linux Shell

### 表 20-6
### ulimit 命令行参数
| 参数 | 说明 |
| :--- | :--- |
| -a | 当前激活的限制 |
| -c | 最大的核心转储大小（KB） |
| -d | 进程最大的数据段大小（KB） |
| -f | 最大的文件块大小（以 512 字节块为单位） |
| -l | 可锁定的最大内存（KB） |
| -m | 可使用的最大物理内存（KB） |
| -n | 进程同时可以打开的文件数 |
| -p | 用户同时可以激活的进程数 |
| -s | 进程最大的栈大小 |
| -t | CPU 时间限制 |
| -H | 显示或设置硬限制 |
| -S | 显示或设置软限制 |

要显示所有当前设置的限制，请使用 -a 参数。

```
$ ulimit -a
time(seconds) unlimited
file(blocks) unlimited
data(kbytes) unlimited
stack(kbytes) 8192
coredump(blocks) 0
memory(kbytes) unlimited
locked(memory(kbytes)) unlimited
process
nofiles 1024
vmemory(kbytes) unlimited
locks unlimited
```

要设置限制，只需在相应的参数后添加限制数量的数字。

```
$ ulimit -f 2
$
```

这为新文件可以包含的块数设置了软限制。如果你尝试创建一个大于限制的文件，shell 将阻止该尝试并显示警告：

```
$ cat datal >> data2
File size limit exceeded
$
```

如果你想为每个用户登录登录 shell 设置限制，可以在 `/etc/profile` 文件中使用 `ulimit` 命令，该文件会在每次登录时运行。这是限制用户系统资源的一种极方法。

## 在 dash 中编写脚本

遗憾的是，dash shell 不识别 bash shell 的所有脚本功能。为 bash 环境编写的脚本在 ash 或 dash shell 上运行时会失败。本节描述了你需要注意的差异，以确保你的脚本能够在 ash 或 dash shell 环境中正常运行。

## 创建 ash 和 dash 脚本

你现在可能猜到，为 ash shell 创建脚本与为 bash shell 创建脚本非常相似。你应该始终在脚本中指定想要使用的 shell，以确保脚本在正确的 shell 中运行。

你可以在 shell 的第一行这样做：

```
#!/bin/ash
```

或者

```
#!/bin/dash
```

你也可以在这一行指定 shell 命令行参数，正如之前在“原始 ash Shell”部分中使用 -e 命令行参数所演示的那样。

## 无法工作的功能

遗憾的是，由于 ash 和 dash shell 是 Bourne shell 特性的子集，bash shell 脚本中的某些功能在 ash 或 dash shell 中无法工作。这些通常被称为 bashisms（bash 特性）。本节简要总结了你可能在 bash 脚本中使用但在 ash 或 dash shell 环境下无法使用的 bash 功能。

## 使用算术运算

第 8 章展示了在 bash 脚本中表示数学运算的三种方法：

ash 和 dash shell 支持 `expr` 命令和双括号方法，但不支持方括号方法。如果你有大量使用方括号的数学运算，这可能会成为问题：

```
$ cat test5
!/bin/dash
# testing
```

（注：原文后续部分存在大量重复的 OCR 错误片段，已根据核心逻辑完成翻译。）
