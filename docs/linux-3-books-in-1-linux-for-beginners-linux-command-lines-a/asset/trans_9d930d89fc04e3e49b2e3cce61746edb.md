

- 您可以使用 C-e 命令移动到当前句子的末尾。
- 您可以使用 C-a 命令移动到当前句子的开头。
- 您可以使用 M-> 命令移动到文本的最后一行。
- 您可以使用 M-< 命令移动到文本的第一行。
- 您可以使用 M-v 命令向后移动一屏数据。
- 您可以使用 C-v 命令向前移动一屏数据。

您可以使用以下命令将编辑器缓冲区保存为文件并退出 emacs 编辑器：

- 您可以使用 C-x C-s 命令将当前缓冲区中已编写的内容保存为文件。
- 您可以使用 C-x C-c 命令退出 emacs 编辑器并停止编辑器的操作。
- 您可以使用 C-z 命令退出 emacs 编辑器。然而，该命令不会保持会话运行，因此您无法返回该会话。

## 编辑数据

Emacs 编辑器在插入和删除文本方面功能强大。插入文本只需将光标移动到您希望插入文本的位置并键入文本即可。退格键用于删除光标位置之前的字符以删除文本。删除键也用于删除光标位置处的字符。

编辑器还提供了删除（kill）文本的选项；删除（delete）和切除（kill）文本之间的区别在于，当文本被切除时，它会被放入一个临时区域，并且可以随时取回，而删除的文本则会被永久移除。Emacs 提供了以下命令来切除文本：

- 您可以使用 M-Backspace 命令切除光标当前位置之前的一个单词。
- 您可以使用 M-k 命令切除从光标当前位置到句子末尾的所有内容。
- 您可以使用 M-D 命令切除光标当前位置之后的一个单词。
- 您可以使用 C-k 命令切除从光标当前位置到该行末尾的所有内容。

您还可以通过将光标移动到要切除部分的开头，按下 C-空格键或 C-@，并将光标放置在部分的末尾来大尺度地切除文本。然后按 C-w，所有指定的文本都会被切除。

## 常用 Linux 命令

要详细讨论的 Linux 命令实在太多了，但我们已经介绍了一些最常见的命令。如果您想了解任何 Linux 命令的功能，只需使用以下语法和命令名称访问其手册页：

```
$ man command-name
```

下表为您展示了更多命令，包括它们的语法以及对它们功能的描述：

| 命令 | 语法 | 描述 |
| :--- | :--- | :--- |
| adduser/addgroup | $ sudo adduser $ sudo addgroup | 这两个命令分别向系统添加用户或组 |
| agetty | $ agetty -L 9600 ttyS1 vt100 | 一个管理虚拟和物理终端的程序。由 init 调用，当建立连接时打开 tty 端口 |
| alias | $ alias home='cd' | 为特定的 Linux 命令创建快捷方式或别名 |
| apropos | $ apropos adduser | 搜索并显示命令或程序的手册页描述 |
| apt | $ sudo apt update | Ubuntu 和 Debian 系统的高级包管理器 |
| apt-get | $ sudo apt-get update | 用于安装、移除和升级软件包以及升级操作系统 |
| aptitude | $ sudo aptitude update | 基于文本的 GNU/Linux 包管理系统，用于安装或移除软件包 |
| arch | $ arch | 显示机器硬件或架构名称 |
| arp | $ sudo arp-scan | ARP 将 IP 网络地址映射到 MAC 地址 – 此命令扫描指定网络上的所有活动主机 |
| at | $ sudo at | 安排任务在未来指定的时间执行 |
| atq | $ atq | 用于查看在 at 命令中排队的任务 |
| atrm | $ atrm (job number) | 用于根据任务编号从 at 命令队列中删除任务 |
| awk | $ awk '' | 一种用于处理文本以及作为报告和数据提取工具的程序 |
| basename | $ basename bin/findhosts.sh | 打印去除绝对路径中目录的文件名 |
| bc | $ echo 20.05 + 15.00 \| bc | 强大的递归 CLI 计算器语言 - 参见语法下的示例 |
| bzip2 | $ bzip2 -z filename<br>$ bzip2 -d filename.bz2 | 压缩或解压指定的文件 |
| cal | $ cal | 打印日历 |
| cat | $ cat file.txt | 查看文件内容，连接文件或数据并显示 |
| chgrp | $ chgrp (new) (old) | 更改文件的组所有权。先提供新名称，后提供现有名称 |
| chmod | $ chmod | 更改或更新指定文件的访问权限 |
| chown | $ chown | 更改或更新目录或文件的组和用户所有权 |
| cksum | $ cksum | 显示输入文件的字节计数和 CRC 校验和 |
| clear | $ clear | 清屏 |
| cmp | $ cmp file1 file2 | 逐字节比较两个文件 |
| comm | $ comm file1 file2 | 按行比较已排序的文件 |
| cp | $ cp | 将目录和文件从一个位置复制到另一个位置 – 必须指定位置 |
| date | $ date | 显示和设置系统时间和日期 |
| df | $ df -h | 显示指定文件系统的磁盘空间使用情况 |
| diff | $ diff file1 file2 | 逐行比较指定文件，还可以查找和定位目录之间的差异 |
| dir | $ dir | 类似于 ls 命令，它列出目录内容 |
| dmidecode | $ sudo dmidecode | 检索有关 Linux 系统硬件的信息 |
| du | $ du | 显示文件在目录及相关子目录中如何使用磁盘空间 |
| echo | $ echo | 获取指定的文本行并打印它 |
| eject | $ eject | 弹出 DVD、CD ROM 和其他可移动介质 |
| env | $ env | 列出和设置当前环境变量 |
| exit | $ exit | 退出 shell |
| expr | $ expr | 计算指定的表达式 |
| factor | $ factor | 显示指定数字的质因数 |
| find | $ find | 使用用户、权限、数据、文件类型大小等属性在目录和子目录中搜索指定文件 |
| free | $ free | 显示系统的内存使用情况。在命令中添加 -h 以人类可读格式显示信息 |
| grep | $ grep | 在文件中搜索指定模式并显示包含该模式的行 |
| groups | $ groups | 显示指定用户所属的组 |
| gzip | $ gzip | 压缩指定文件并将其替换为带有 .gz 扩展名的文件 |
| gunzip | $ gunzip | 展开/还原使用 gzip 压缩的文件 |
| head | $ head (file or stdin) | 显示指定的文件或 stdin 的前 10 行 |
| history | $ history | 显示命令或检索用户已经执行的命令的信息 |
| hostname | $ hostname | 打印或设置 Linux 系统主机名 |
| hostnamectl | $ hostnamectl | 控制系统主机名并修改或打印主机名及相关设置 |
| hwclock | $ sudo hwclock | 管理硬件时钟并读取或设置它 |
| hwinfo | $ hwinfo | 查看系统以了解硬件配置 |
| id | $ id | 显示当前或指定用户名的组和用户信息 |
| ifconfig | $ ifconfig | 配置、查看和控制指定 Linux 系统的网络接口 |
| ionice | $ ionice | 设置/查看进程 I/O 调度类和指定进程优先级 |
| iostat | $ iostat | 显示分区和设备的输入/输出和 CPU 统计信息，并生成关于如何更新配置以实现输入/输出平衡的报告 |
| ip | $ sudo ip | 显示/管理设备、路由、隧道和策略路由 |

