
- Linux 内核在 `/proc/PID/fd/` 中为进程打开的每个文件保持符号链接，其中 `PID` 是对应进程的标识号。系统管理员如何利用该目录来验证由 `nginx` 打开的日志文件位置，假设其 PID 为 `1234`？

通过执行命令 `ls -l /proc/1234/fd/`，这将显示目录中每个符号链接的目标。

- 仅使用 Shell 内置命令就可以执行算术计算，但浮点运算需要特定的程序，如 `bc`（*基础计算器*）。使用 `bc` 甚至可以通过参数 `scale` 指定小数位数。然而，`bc` 仅通过其标准输入接受操作，通常是在交互模式下输入。使用 Here 字符串，如何可以将浮点运算 `scale=6; 1/3` 发送到 `bc` 的标准输入？

```bash
$ bc <<<"scale=6; 1/3"
```

![img/824749d5fc1d265354d0e66a01af9ced_287_0.png](img/824749d5fc1d265354d0e66a01af9ced_287_0.png)

# 103.4 第 2 课

| **证书：** | LPIC-1 (101) |
| :--- | :--- |
| **版本：** | 5.0 |
| **主题：** | 103 GNU 和 Unix 命令 |
| **目标：** | 103.4 使用流、管道和重定向 |
| **课程：** | 2/2 |

## 引言

Unix 哲学的一个方面规定，每个程序应该有一个特定的用途，并且不应该试图整合其范围之外的功能。但保持简单并不意味着结果不细致，因为不同的程序可以串联起来以产生组合输出。垂直线字符 `|`，也称为*管道*符号，可用于创建一个管道，将一个程序的输出直接连接到另一个程序的输入，而*命令替换*允许将程序的输出存储在变量中，或将其直接用作另一个命令的参数。

## 管道

与重定向不同，管道中的数据从左到右流动，目标是另一个进程，而不是文件系统路径、文件描述符或 Here 文档。管道字符 `|` 告诉 Shell 同时启动所有不同的命令，并将前一个命令的输出连接到下一个命令的输入，从左到右。例如，不使用重定向，`cat` 发送到标准输出的文件 `/proc/cpuinfo` 的内容可以通过以下命令管道传输到 `wc` 的 stdin：

```bash
$ cat /proc/cpuinfo | wc
208   1184   6096
```

在没有文件路径的情况下，`wc` 计算其 stdin 接收到的行数、单词数和字符数，如示例所示。复合命令中可能存在多个管道。在下面的示例中，使用了两个管道：

```bash
$ cat /proc/cpuinfo | grep 'model name' | uniq
model name        : Intel(R) Xeon(R) CPU        X5355 @ 2.66GHz
```

由 `cat /proc/cpuinfo` 产生的文件 `/proc/cpuinfo` 的内容被管道传输到命令 `grep 'model name'`，该命令随后仅选择包含术语 `model name` 的行。运行示例的机器有许多 CPU，因此存在带有 `model name` 的重复行。最后一个管道将 `grep 'model name'` 连接到 `uniq`，后者负责跳过任何与前行相等的行。

管道可以与重定向在同一命令行中组合。前面的示例可以重写为更简单的形式：

```bash
$ grep 'model name' </proc/cpuinfo | uniq
model name        : Intel(R) Xeon(R) CPU        X5355 @ 2.66GHz
```

`grep` 的输入重定向并非严格必要，因为 `grep` 接受文件路径作为参数，但该示例演示了如何构建此类组合命令。

管道和重定向是互斥的，即一个源只能映射到一个目标。然而，可以使用程序 `tee` 将输出重定向到文件并在屏幕上看到它。为此，第一个程序将其输出发送到 `tee` 的 stdin，并向后者提供文件名以存储数据：

```bash
$ grep 'model name' </proc/cpuinfo | uniq | tee cpu_model.txt
model name        : Intel(R) Xeon(R) CPU        X5355 @ 2.66GHz
$ cat cpu_model.txt
model name        : Intel(R) Xeon(R) CPU        X5355 @ 2.66GHz
```

链中最后一个程序（由 `uniq` 生成）的输出被显示并存储在文件 `cpu_model.txt` 中。为了在提供文件时不覆盖其内容而是向其中追加数据，必须向 `tee` 提供选项 `-a`。

进程的标准输出会被管道捕获。假设你需要在屏幕上经历一个漫长的编译过程，同时希望将标准输出和标准错误都保存到一个文件中以便后续检查。假设当前目录中没有 *Makefile*，以下命令将输出错误：

```
$ make | tee log.txt
make: *** No targets specified and no makefile found.  Stop.
```

虽然错误消息显示在了屏幕上，但 *make* 生成的错误消息并未被 *tee* 捕获，文件 *log.txt* 被创建为空。在管道捕获 stderr 之前，需要进行重定向：

```
$ make 2>&1 | tee log.txt
make: *** No targets specified and no makefile found.  Stop.
$ cat log.txt
make: *** No targets specified and no makefile found.  Stop.
```

在这个例子中，*make* 的 stderr 被重定向到了 stdout，因此 *tee* 能够捕获它，在屏幕上显示并将其保存到文件 `log.txt` 中。在这种情况下，保存错误消息以便后续检查可能很有用。

## 命令替换

捕获命令输出的另一种方法是*命令替换*。通过将命令放在反引号内，Bash 会将其替换为其标准输出。以下示例展示了如何将一个程序的 stdout 用作另一个程序的参数：

```
$ mkdir `date +%Y-%m-%d`
$ ls
2019-09-05
```

程序 *date* 的输出，即格式化为 *年-月-日* 的当前日期，被用作 *mkdir* 创建目录的参数。使用 `$( )` 代替反引号也可以获得相同的结果：

```
$ rmdir 2019-09-05
$ mkdir $(date +%Y-%m-%d)
$ ls
2019-09-05
```

同样的方法也可以用于将命令的输出存储为变量：

```
$ OS=`uname -o`
$ echo $OS
GNU/Linux
```

命令 `uname -o` 输出当前操作系统的通用名称，该名称被存储在会话变量 `OS` 中。将命令的输出赋值给变量在脚本中非常有用，这使得可以以多种不同的方式存储和评估数据。

根据被替换命令生成的输出，内建命令替换可能并不合适。一种更高级的方法是使用程序输出作为另一个程序参数，采用名为 `xargs` 的中间工具。程序 `xargs` 使用通过 stdin 接收的内容，将这些内容作为参数运行给定的命令。以下示例展示了 `xargs` 运行程序 `identify`，其参数由程序 `find` 提供：

```
$ find /usr/share/icons -name 'debian*' | xargs identify -format "f: %wx%h\n"
debian-swirl.svg: 48x48
debian-swirl.png: 22x22
debian-swirl.png: 32x32
debian-swirl.png: 256x256
debian-swirl.png: 48x48
debian-swirl.png: 16x16
debian-swirl.png: 24x24
debian-swirl.svg: 48x48
```

程序 `identify` 是 *ImageMagick* 的一部分，*ImageMagick* 是一组用于检查、转换和编辑大多数图像文件类型的命令行工具。在示例中，`xargs` 获取了 `find` 列出的所有路径，并将它们作为参数传递给 `identify`，`identify` 随后按照选项 `-format` 的要求格式显示每个文件的信息。示例中 `find` 找到的文件是包含 Debian 文件系统中发行版标志的图像。`-format` 是 `identify` 的参数，而不是 `xargs` 的参数。
