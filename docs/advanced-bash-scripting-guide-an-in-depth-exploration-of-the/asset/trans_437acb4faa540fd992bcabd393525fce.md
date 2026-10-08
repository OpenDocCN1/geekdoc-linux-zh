

# 高级 Bash 脚本指南

objdump
以十六进制形式或反汇编列表（使用 -d 选项）显示对象文件或可执行二进制文件的信息。

```bash
bash objdump -d /bin/ls
/bin/ls:    file format elf32-1386

section .init 的反汇编:

080490bc.<init>:
080490bc:    55      push %ebp
080490bd:      e9 e5    mov %esp,%ebp
```

mookie
该命令生成一个“魔法饼奇”（magic cookie），这是一种 128 位（32 字符）的伪随机十六进制数，通常用作 X 服务器的授权“签名”。它也可以在脚本中使用，作为一种“快速且粗略”的随机数。

```bash
random000=$(mookie)
当然，脚本也可以使用 md5sum 来实现相同的目的。

# 对脚本本身生成 md5 校验和。
random001=$(md5sum $ | awk '{print $1}')
# 使用 'awk' 去掉文件名。
mookie 命令提供了另一种生成“唯一”文件名的方法。
```

# 示例 16-62 文件名生成器

```bash
#!/bin/bash
# tempfile-name.sh:   临时文件名生成器
BASE_STR=`mookie`      # 32 字符魔法饼奇。
# 魔法饼奇字符串中的任意位置。
POS=1                 # 获取 LEN 个的字符。
LEN=5
prefix=temp           # 毕竟，这是一个“临时”文件。
# 为了更具“唯一性”，可以使用与下方
# 相同的方法来生成
#++ 前缀。
suffix=${BASE_STR:$POS:$LEN}  # 提取从位置 11 开始的
#++ 的 5 字符字符串。
tempfile-name=$prefix.$suffix  # 构造文件名。
echo "Temp filename = "$tempfile_name"

# sh tempfile-name.sh
# Temp filename = temp.el9ea

# 将此生成“唯一”文件名的方法
#++ 与 ex51.sh 中的 'date' 方法进行比较。

exit 0
```

第 16 章 外部过滤器、程序和命令

# 高级 Bash 脚本指南

units
此工具在不同的单位之间进行转换。虽然通常在交互模式下调用，但在脚本也可以发现 units。

# 示例 16-63 将米转换为里

```bash
#!/bin/bash
# 已安装 unit-conversion.sh 工具。
# 必须有 'units' 命令

convert_units () # 接收要转换的单位作为参数。
{
  cf=$$(units "$1" "$2" | sed --silent -e 'lp' | awk 'print $2')
  # 去掉实际转换因子以外的所有内容。
  echo "$cf"
}
Unit1=miles
Unit2=meters
factor=convert_units $Unit1 $Unit2
quantity=3.73

result=$(echo $quantity | bc)
echo "There are $result $Unit2 in $quantity $Unit1."

# 如果向函数传递不兼容的单位，
#+ 例如“亩”和“英里”，会什么？

echo 0

# 练习：编辑此脚本以接受命令行参数，
#  当然，还需要适当的错误检查。
```

m4
m4 是一种隐藏的尺度，是一个强大的宏处理过滤器，几乎是一门完整的语言。虽然它最初是作为 RatFor 的预处理器编写的，但 m4 证明是一个独立的工具。事实上，m4 结合了 eval、tr 和 awk 的功能，此外还有丰富的宏扩展功能。

Linux Journal 2002 年 4 月版有一篇关于 m4 及其用很好的文章。

# 示例 16-64 使用 m4

```bash
#!/bin/bash
# m4.sh: 使用 m4 宏处理器

# 字符串
string=abcdA01
echo len($string) | m4              # 7
echo substr($string, 4) | m4      # A01
echo regexp($string, [0-1],\|&Z) | m4  # 01Z

# 算术
var=99
echo incr($var) | m4                  # 100
```

第 16 章 外部过滤器、程序和命令 316

# 高级 Bash 脚本指南

```bash
echo "eval($var / 3)" | m4      # 33
exit
```

xmessage
这种 echo 的 X 基础变体会在桌面上弹出一个消息/查询。

```bash
xmessage Left click to continue -button okay
```

zenity
zenity 工具擅长显示 GTK+ 对话框组件，非常适合脚本用途。

doexec
doexec 命令允许向二进制可执行文件传递任意参数列表。特别是，传递 argv[0]（对应于脚本中的 $0）允许它以不同的名称被调用，然后它可以根据调用时使用的名称携带不同的动作集。这种向可执行文件传递选项的方法方式有些迂回。

例如，/usr/local/bin 目录可能包含一个名为 "aaa" 的二进制文件。调用 `doexec /usr/local/aaa list` 将列出当前工作目录下所有名为 "aaa" 的文件，而（同一个可执行文件）`doexec /usr/local/bin/aaa delete` 则将删除这些文件。

- 可执行文件的行为可以在执行文件本身的代码中定义，类似于下面的内容：

```bash
case $0 in
  *name1 ) do_something;
  *name2 ) do_something_else;
  *name3 ) do_another_thing;
  ) bail_out;
esac
```

dialog
dialog 系列提供了从脚本中调用交互式“对话框”的方法。更复杂的变体 dialog、kdialog 实际上调用了 X 窗口。

sox
sox 或“声音交换”命令播放并对音频文件进行转换。事实上，/usr/bin/play 执行文件（已废弃）只是 sox 的 shell 封装。

例如，soundfile.wav soundfile.au 将 WAV 音频文件转换为（音频格式）AU 文件。

脚本非常适合对音频文件进行批量 sox 操作。例如，Linux Radio Timeshift 和 MP3 项目。

# 第 17 章 系统和管理命令

rc.d 中的启动和关闭脚本说明了许多此类命令的用途（用处）。这些命令通常由 root 调用，用于系统维护或紧急文件修复。请谨慎使用，不当使用某些命令可能会损坏系统。

# 用户和组

users
显示所有登录的用户。这大致相当于 who -q。

groups
列出当前用户及其所属的组。这对应于内部变量 $GROUPS，但给出组名而不是数字。

```bash
bash$ groups
bozita cdrom writer xgrp

bash$ echo $GROUPS
501
```

# chown, chgrp

chown 命令更改文件或文件的所有权。这是一个实用方法，root 可以将所有权从一个用户转移到另一个。普通用户无法更改所有权，即使是自己的文件。

```bash
root# chown bozo *.txt
```

chgrp 命令更改文件或文件的组所有。你必须是文件的所有者也是该组成员。

```bash
bash$ groups
bozita cdrom writer xgrp

bash$ echo $GROUPS
501
```

# 高级 Bash 脚本指南

```bash
bash$ id
501
```

id 命令仅在有效 ID 与实际 ID 不同时显示。

另见示例 9-5。

lid (list ID) 命令显示给定用户所属的组，或者相反显示属于某个组的用户。它只能由 root 调用。

```bash
root# lid bozo
bozo(gid=500)

root# lid daemon
bin(gid=1)
demon(gid=2)
adm(gid=4)
lp(gid=7)
```

