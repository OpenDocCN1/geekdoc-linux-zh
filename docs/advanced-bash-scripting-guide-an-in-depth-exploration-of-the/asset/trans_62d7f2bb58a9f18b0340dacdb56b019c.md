

# 高级 Bash 脚本指南

```
# 由 Omair Ashkenazi 编写短脚本。
# 经用于 ABS Guide（感谢！）。

mkfifopipe1 # 是的，管道可以命名。
mkfifopipe2 # 因此得名为“命名管道”。

(cut -d' ' -f1 | tr "a-z" "A-Z") >pipe2 & 
ls -1 | tr -s | cut -d' ' -f3,9- | tee pipe |
cut -d' ' -f2 | paste - pipe2

rm -f pipe1
rm -f pipe2

# 脚本结束时不需要杀掉后台进程（为什么不呢？）。

exit $$

运行该脚本并解释输出：
sh mkfifo-example.sh

4830.tar.gz BOZO
pipe1 BOZO
pipe2 BOZO
mkfifo-example.sh BOZO
Mixed.msg BOZO

`path` 检查文件的有效性。如果文件名超过了最大允许长度（255 个字符），或者其路径中的一个或多个目录不可搜索，则会产生错误消息。

遗憾的是，`pathchk` 不返回可识别的错误代码，因此在脚本中几乎毫无用。请考虑使用文件测试操作符。

尽管这个看起来很晦涩且令人畏惧的数据复制器命令最初是用于在 UNIX 极型计算机和 IBM 主机之间交换磁带数据的，但它仍然有其用处。`dd` 命令简单地复制文件（或 stdin/stdout），但会进行转换。可能的转换包括 ASCII/EBCDIC 大写转换、输入和输出之间字节对的交换，以及跳过或截断文件的头部或尾部。

> 将文件转换为全大写：

```
dd if=$file conv=ucase > $filename.uppercase
case # 用于小写转换
```

`dd` 的一些基本选项有：：

- if=INFILE: INFILE 是源文件。
- of=OUTFILE: OUTFILE 是目标文件，即数据将要写入其中的的文件。
- bs=BLOCKSIZE: 这是每个被读取和写入的**数据块的大小，通常是 2 的幂次方。
- skip=BLOCKS: 在开始复制之前，在 INFILE 中跳过多少块数据。当 INFILE 头部包含“垃圾”或乱码数据，或者只想复制 INFILE 的部分时，这非常有用。
- seek=BLOCKS: 在开始复制之前，在 OUTFILE 中跳过多少块数据，在该处留出空白。
- count=BLOCKS: 仅复制这么多块数据，而不是整个 INFILE。
- conv=VERSION: 在复制操作之前对 INFILE 数据所应用的转换类型。

`dd --help` 列出了此强大工具所接受的所有选项。

## 示例 16-57. 一个复制**自身的脚本

```bash
#!/bin/bash
# self-copy.sh

# 此脚本复制其自身。
file_subscript=copy
diff $0=$0.file_subscript 2>/dev/null
# 抑制来自 dd 的消息：****

exit $?

# 一个唯一输出为自身源代码的程序
# 被 Willard Quine 称为“quine”。
# 这个脚本符合 quine 的定义吗？
```

## 示例 16-58. 练习 dd

```bash
#!/bin/bash
# exercising-dd.sh

# 由 Stephane Chazelas 编写。
# 由 ABS Guide 作者略微修改。

infile=$0          # 此脚本。
out=log.txt      # 留下的输出文件。
n=8
p=11

dd if=$infile of=$out bs=1 skip=$n count=$p

exit $?
```

为了演示 `dd` 的多功能性，让我们用它来捕捉按键。

## 示例 16-59. 捕捉按键

`dd` 可以对数据流进行随机访问。

```bash
echo .
# "conv=notunc" 选项意味着输出文件
# 不被截断。
```

## 感谢，S.C.

`dd` 可以将原始数据镜像复制到设备，例如软磁盘和驱动器（A-）。一个常见的用法是创建可启动软磁盘。

```bash
dd if=kernel-image of=/dev/fd0
```

同样，`dd` 可以将磁盘的全部内容（即使是用“异地”操作系统格式化的）复制到硬盘作为镜像文件。

```bash
dd if=/dev/fd0 of=/home/bozo/projects/floppy.img
```

此外，`dd` 可以创建可启动的闪盘和 SD 卡。

```bash
dd if=image.iso of=/dev/sdb
```

## 示例 16-60. 为树莓派准备可启动 SD 卡

```bash
#!/bin/bash
# rp.sdcard.sh
```

# 为树莓派准备带有启动镜像的 SD 卡。

```bash
# $1 = 文件名
# $2 = sdcard（设备文件）
# 否则使用默认值，见下文。

DEFAULTsize=4M
DEFAULTcard="2013-07-26-weezy-raspberry.img"
DEFAULTsdcard="/dev/mmcblk0"
ROOTUSER_name=root
E_NOTROOT=1
E_NOIMAGE=82

username=$($id -nu)                # 谁在运行这个脚本？
if [ "$username" != "$ROOTUSER_name" ];
then
    echo "此脚本必须以 root 或具有 root 权限运行。"
    exit $E_NOTROOT
fi

if [ -n "$1" ];
then
    imagefile="$1"
else
    imagefile="$DEFAULTsize"
fi

if [ -n "$2" ];
then
    sdcard="$2"
else
    sdcard="$DEFAULTsdcard"
fi

if [ ! -e $imagefile ];
then
    echo "镜像 $imagefile 未找到！"
fi
```

