
root@itlaptop:~/media/phil/90c41808-4025-46b4-b220-76d4f325# `ls`

`bin` `lib64` `sbin`

root@itlaptop:~/media/phil/90c41808-4025-46b4-b220-76d4f325# `exec` `bin/bash`

root@itlaptop:~/media/phil/90c41808-4025-46b4-b220-76d4f325#

### 图 2.6
### 将路径指向良好的路径。

### 图 2.7
### 将库路径指向良好的库。

接收到文件结束（EOF）标记。`netcat` 的 `-k` 选项会让监听器保持运行，直到你在启动 `netcat` 的终端中按下 Control-C 为止。启动日志监听器的命令是 `netcat -k -l {port} >> {log file}`，即 `netcat -k -l >> example-log.txt`。该命令如图 2.8 所示。请注意，虽然我在这里使用了 `netcat`，但它是大多数系统上 `nc` 指向同一个程序的符号链接，因此你可以使用你偏喜的任何一个。

```
phil@laptop:~$ netcat -k -l 9999 >> example-log.txt
```

图 2.8
在取证工作站上运行 `netcat` 监听器。

### 从受控系统发送数据

现在你已经在取证工作站上有了一个监听器，使用 `netcat` 跨网络发送数据变得简单了。发送内容记录的通用序列是 `{command} | nc forensic workstation IP {port}`。对于没有产生明显输出的命令，你可能想在发送命令输出之前，使用 `echo` 实用程序发送某种头部。这在图 2.9 中所示。运行图 2.9 所示命令的结果如图 2.10 所示。本章稍后将讨论如何使用脚本来此此过程。

图 2.9

使用 `netcat` 向取证工作站发送信息。

```
phil@i7laptop:-$ netcat -k -l 9999 >> example-log.txt

C

phil@i7laptop:-$ cat example-log.txt

Subject date/time:

tue Nov 20 22:46:18 EDT 2015

phil@i7laptop:--$ 
```

图 2.10
监听器从图 2.9 的命令中收到的结果。

### 发送文件

从受控系统中提取可疑文件进行进一步研究并不罕见。`netcat` 在执行此任务时非常方便。为了接收文件，你应该在取证工作站上启动一个新的不使用 `-k` 选项的监听器。在这种情况下，你希望在文件传输后结束监听器。命令是 `nc -l {port} > {filename}`。

在受控系统上，可疑文件被重定向到 `netcat` 发送端。发送文件的语法是 `nc {forensic workstation IP} {port} < {filename}`，即 `nc 192.168.1.119 4444 < /bin/bash`。此文件传输的监听器和发送端分别如图 2.11 和图 2.12 所示。

```
phil@it1laptop:~$ nc -l 4444 > bash.suspect

phil@it1laptop:~$ ls bash.suspect

bash.suspect

phil@it1laptop:~$ chmod +x bash.suspect

phil@it1laptop:~$ /bash.suspect

phil@it1laptop:~$ 
```

### 图 2.11

设置 `netcat` 监听器接收文件。

```
phil@laptop:~$ nc 192.168.1.119 4444 < /bin/bash

phil@laptop:~$ _
```

图 2.12

使用 `netcat` 发送文件。

### 使用脚本自动化过程

显而易见，我们上面描述的这个小 `netcat` 系统非常适合编写脚本。人们可能会提出的第一个问题是应该使用哪种脚本语言。许多人会立即跳到使用 Python 来完成这项任务。虽然我喜欢用 Python 处理许多取证和安全任务，但在这种情况下并不是最佳选择。

在我看来，有几个理由说明 shell 脚本是更好的选择。首先，我们希望尽可能地减少内存占用，而执行 Python 解释器与这一目标背道而驰。其次，主要运行其他程序的 Python 脚本毫无意义。直接在 shell 脚本中执行这些程序要简单得多。对于某些读者来说，额外的好处是这里描述的脚本构成了基础 shell 脚本的很好的介绍。

### 编写服务器脚本

下面的脚本将为案件文件创建一个新目录并启动两个监听器。第一个监听器用于记录在受控（客户端）机器上执行的命令，第二个用于接收文件。还提供了一个清理并关闭监听器的脚本。这里是主脚本 `start-case.sh`：

```bash
#!/bin/bash

#

### start-case.sh

#
```

### 在取证工作站上启动新案件的简单脚本。如果需要将创建一个新文件夹
### 并启动两个监听器：用于日志信息
### 另一个用于接收文件。旨在作为
### 初始现场响应的一部分。
### 由 Dr. Phil Polstra (@ppolstra) 编写，专为
### PentesterAcademy.com。

```
usage () {

echo "usage: $0 <case number>"

echo "创建案件文件夹并启动监听器的简单脚本"

exit 1

}

if [ $# -lt 1 ]; then

usage

else

echo "Starting case $1"

fi

### 如果目录不存在则创建它

if [ ! -d $1 ]; then

mkdir $1

fi

### 创建日志监听器

nc -k -l 4444 >> $1/log.txt &

echo "Started log listener for case $1 on $(date)"

### 启动文件监听器

./start-file-listener.sh $1 &
```

此脚本以特殊注释 `#!` 开头，称为 she-bang，它会导致 `bash` 被执行。运行特定的 shell 是重要的，因为允许用户自行选择 shell 的可能会选择与你的脚本不兼容的内容。行中的任何位置开始都是注释，在行尾结束。前几行是描述脚本的注释。定义了一个名为 `usage` 的函数。在 shell 脚本中定义函数只需输入其名称，后跟一个空格、空括号，然后用大括号将函数中的命令括起来。与编译语言和脚本语言不同，shell 脚本需要在适当的位置留有空白，否则它们将无法正常工作。`usage: $0 <case number>` 一行中的 `$0` 是一个变量，它被设置为运行脚本时使用的第一个参数，即文件名。注意 `echo` 命令中使用了双引号。任何包含在双引号内的内容都会被 shell 扩展（解释）。如果使用单引号，则不进行扩展。当用户提供的命令行参数没有意义时，定义一个显示出来的 `usage` 函数是良好的编程习惯。`if [ $# -lt 1 ] then` 行开启了一个 `if` 块。逻辑测试包含在方括号中。注意括号周围和部分之间必须有空格。

### 脚本服务器

```bash
#!/bin/bash

#

### start-case.sh

#
```

# 启动新案件的简单脚本。如果需要将创建一个新文件夹
# 并启动两个监听器：一个用于日志信息
### 另一个用于接收文件。旨在作为
### 初始现场响应的一部分。
### 由 Dr. Phil Polstra (@ppolstra) 编写，专为
### PentesterAcademy.com。

```
usage () {

echo "usage: $0 <case number>"

echo "创建案件文件夹并启动监听器的简单脚本"

exit 1

}

if [ $# -lt 1 ]; then

usage

else

echo "Starting case $1"

fi

### 如果目录不存在则创建它

if [ ! -d $1 ]; then

mkdir $1

fi

### 创建日志监听器

nc -k -l 4444 >> $1/log.txt &

echo "Started log listener for case $1 on $(date)"

### 启动文件监听器

./start-file-listener.sh $1 &
```
