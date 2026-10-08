

# cksum

# 退出状态

0

命令执行成功且所有请求的更改已完成。

>0

发生错误。

# 文件

/etc/passwd

系统密码文件。

# 属性

有关以下属性的描述请参见 attributes(5)：

| 属性类型 | 属性值 |
| --- | --- |
| Availability | SUNWcs |
| CSI | Enabled |

> \mdash; chown 支持 CSI，所有者和组除外

# 参见

chgrp(1), chmod(1), chown(2), fpathconf(2), passwd(4), system(4), attributes(5), environ(5), largefile(5)

# cksum — 写入文件校验和和大小

# 概要

```
/usr/bin/cksum [file...]
```

# 描述

cksum 命令计算并向标准输出每个输入文件的循环冗余校验 (CRC)，并向标准输出写入每个文件中字节的冗余。

对于每个成功处理的文件，cksum 按照以下格式写入：
"%u %d %s\n" 校验和，字节数，路径名

> 如果未指定文件操作数，则省略路径和前导空格。CRC 基于参考以太网标准中用于 CRC 检查的多项式。

CRC 校验和的编码由生成多项式定义：

```
G(x) = x32 + x26 + x23 + x22 + x16 + x12 + x11 + x10 + x8 + x7 + x4
+ x2 + x + 1
```

# cksum

从数学上，给定文件对应的 CRC 值由以下步骤定义。

1. 待评估的 $n$ 位被视为阶为 $n-1$ 的模 2 多项式 M(x) 的系数。这 $n$ 位是文件的位；最高位是第一个字节的最高位，最后一位是最后一个字节的最低位（在必要时补零位以达到整数数量的字节数），其中用一个或多个字节的二进制值表示文件的长度，且最低位字节在前。使用能够表示此整数的最少字节数。
2. M(x) 乘以 32（即左移 32 位）并除以 G(x) 进行模 2 除法，产生阶 < 31 的余数 R(x)。
3. R(x) 的系数被视为一个 32 位序列。
4. 对位序列取反，结果即为 CRC。

# 示例

你可以显示单个文件或目录的校验和、列表列表或目录下所有文件的校验和。以下示例显示了当前工作目录下所有目录和文件的校验和。

```
cksum *
18377840 1024 Art
284965401 512 DeadLetters
424967295 0 Design.book
364878112 512 Mail
181174335 737 bibliography
2113126963 526 commands
341495280 934 examples
424967295 0 file
2520900578 12 file1
304812797 241 file2
599640525 242 kookaburra
304812797 241 kookaburral
2464961294 242 kookaburra2
40181032 483 kookaburra3
159814179 2007 listfile
766785258 124 local.cshrc
138306002 560 local.profile
50931726 85 mycode
2025597153 3673 permissions
3135107960 4182 printing
136572283 18 script
1580610504 20 sortfile
1681251586 20 sortoutput
2655897922 23 template
2618551756 84 typescript
2176151109 40020 whpaper.html
cksum*
```

# clear — 清除屏幕

# 概要

```
/usr/bin/clear
```

# 描述

clear 命令在可以的情况下清空你的屏幕或当前的 shell 窗口。它会在环境变量中查找终端类型，然后在 terminfo 数据库中查找如何清空屏幕。

# 属性

有关以下属性的描述请参见 attributes(5)：

| 属性类型 | 属性值 |
| --- | --- |
| Availability | SUNWcsu |

# 参见

attributes(5)

# cmp — 比较两个文件

# 概要

```
/usr/bin/cmp [-l] [-s] file1 file2 [skip1]
```

# 描述

使用 cmp 比较两个文件。如果文件相同，cmp 不产生输出。默认情况下，cmp 会输出文件不同的第一行、该行的字节数以及不同的字符。如果你使用 -l 选项，cmp 只打印文件不同的行号。如果你使用 -s 选项，cmp 会比较文件但不产生输出。如果你使用 -n skip1 选项，cmp 将跳过前 skip1 个字节。

# 选项

- -l 仅打印文件不同的行号。
- -s 比较文件但不产生输出。
- -n skip1 跳过前 skip1 个字节。
- -y 逐行比较文件。

# 操作数

- file1 要比较的第一个文件。
- file2 要比较的第二个文件。
- [skip1] 跳过前 skip1 个字节。

# 使用

cmp [-l] [-s] [-n skip1] [-y] file1 file2 [skip1]

