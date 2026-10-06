

# 高级 Bash 脚本指南

按照习惯，命令从 fd 0 (stdin) 读取输入，将正常输出打印到 fd 1 (stdout)，并将错误输出打印到 fd 2 (stderr)。如果这些文件描述符 (fd) 中的一个没有打开，你可能会遇到问题：

```bash
bash cat /etc/passwd >&-
cat: standard output: bad file descriptor
```

例如，当 xterm 运行时，它会先进行初始化。在运行用户的 shell 之前，xterm 会打开终端设备（`/dev/pts/n` 或类似设备）三次。

此时，Bash 继承了这三个文件描述符，而由 Bash 运行的命令（子进程）也会按继继承这些符，除非你对命令进行了重定向。重定向意味着将其中一个文件描述符重新分配给另一个（通过管道或任何类似机制）。文件描述符可以针对某个命令、子 shell、`while` 或 `if` 循环进行局部重新分配，也可以全局地在 shell 的剩余运行时间内进行重新分配（使用 `exec`）。

`ls > /dev/null` 意味着运行 `ls` 时将 fd 1 连接到 `/dev/null`。

```bash
bash exec 2>/dev/null
bash lsof -a p -- -d0,1
COMMAND PID USER FD TYPE DEVICE SIZE NAME
lsof 3621 0u CH 136,1 3 /dev/pts/1
lsof 3620 1u CH 136,1 3 /dev/pts/1
lsof 3620 2w CH 136,1 120 /dev/null
```

```bash
bash bash -c 'lsof -a p -- -d0,1,2' | cat
COMMAND PID USER FD TYPE DEVICE SIZE NAME
lsof 3709 0u CH 136,1 3 /dev/pts/1
lsof 3709 1u CH 136,1 3 /dev/pts/1
lsof 3709 2w CH 136,1 3 /dev/pts/1
```

```bash
bash echo "$(lsof -a p -- -d0,1,2)" >&6
COMMAND PID USER FD TYPE DEVICE SIZE NAME
lsof 4226 0u CH 136,1 3 /dev/pts/1
lsof 4226 1w FIFO 0,0 7520 pipe
lsof 4226 2w FIFO 0,0 7520 pipe
```

这种方法适用于各种类型的重定向。

# 练习：分析以下脚本。

```bash
#! /usr/bin/env bash
mkfifo /tmp/fifo1 /tmp/fifo2
while read a; do echo "FIFO1: $a"; done < /tmp/fifo1 &
? exec 7 > /tmp/fifo1
exec 8>(while read a; do echo "FD8: $a, to fd7"; done >&7)
```

## 附录 A.I/O 和 I/O 重定向详细介绍

```bash
exec 3>&1
(
  while read a; do echo "FIFO2: $a"; done < /tmp/fifo2 | tee /stderr | tee /dev/4 | tee |
  exec 3> /tmp/fifo2
)

echo 1st, to stdout
sleep 1
echo 2nd, to stderr >&2
sleep 1
echo 3rd, to fd 3 >&3
sleep 1
echo 4th, to fd 4 <&4
sleep 1
echo 5th, to fd 5 >&5
sleep 1
echo 6th, through a pipe | sed 's/.*/PIPE: &, to fd 5/' >&5
sleep 1
echo 7th, to fd 6 <&6
sleep 1
echo 8th, to fd 7 >&7
sleep 1
echo 9th, to fd 8 >&8
) 4>&1 3<-\ | while read a; do echo "FD4: $a"; done 1>&3 5<&- 6<&-
) 5>&1 >3 | while read a; do echo "FD5: $a"; done 1>&3 6<&-
) 6>&1 >3 | while read a; do echo "FD6: $a"; done 3>&-
rm -f /tmp/fifo1 /tmp/fifo2
```

```bash
# 对于每个命令和子 shell，找出哪个 fd 指向什么。

exit 0
```

## 附录 E. 本地化

本地化是一个未文档说明的 Bash 特性。

本地化的 shell 脚本将根据系统区域设置（locale）定义的语言导出其文本。位于德国柏林的 Linux 用户将获得德语脚本输出，而他位于美国马里兰州柏林的表哥将获得来自同一份脚本的英语输出。

要创建一个本地化脚本，请使用以下模板向用户写入所有消息（错误信息、提示信息等）。

```bash
#!/bin/bash
# localized.sh

E_CERROR=65

error() {
  printf "%s" $@ >&2
  exit $E_CERROR
}
```

```bash
cd $var || error "Can't cd to %s." "$var"
read -p $"Enter the value: " var
#
```

```bash
bash -D localized.sh
"Can't cd to %s."
"Enter the value: "
```

这列出了所有本地化文本。`-D` 选项可以在不执行脚本的情况下列出带有 `$` 前缀的双引号字符串。

