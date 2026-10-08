

# uuencode, uudecode — 编码或解码二进制文件

## 概要

```
/usr/bin/uuencode [source-file] decode-pathname
/usr/bin/uudecode [-p] encoded-file
```

## 描述

使用 uuencode/uudecode 命令在 ASCII 和二进制数据之间进行转换。

> 警告 — 如果你在同一目录下运行 uuencode 然后再次对该文件运行 uudecode，你将覆盖原始文件。

### uuencode
uuencode 将二进制文件转换为编码表示，你可以使用 mail(1) 发送该文件。它对 source-file 的内容，或者在未指定 source-file-argument 的情况下对标准输入进行编码。decode-pathname 参数是必须的。decode-pathname 包含在编码文件的头信息中，作为 uuencode 存放二进制（编码）数据的文件名。uudecode 还包含 source-file 的权限模式（setuid、setgid 和粘滞位除外），以便 decode-pathname 以相同的权限模式重新创建文件。

> 注意 — 由于编码后的文件大小扩大了 35%（3 字节变为 4 字节，加上控制信息），其传输时间比等量的二进制文件长。

### uudecode
uudecode 读取 encoded-file，剥离邮件处理程序添加的任何开头和结尾行，并根据头信息中指定的文件名和模式重建原始二进制数据。

编码文件是一个普通的、可移植的、字符集文本文件；你可以使用任何文本编辑器编辑它。最好只更改头信息中的模式或 decode-pathname，以避免破坏解码后的二进制文件。

> 注意 — 调用 uudecode 的远程系统用户（通常是 uucp）必须对 decode-pathname 操作数中指定的文件具有写权限。

## 选项

### uudecode

- -p 解码 encoded-file 并将其作为文件名发送到标准输出。此选项允许你在管道中使用 uuencode。

## uudecode, uudecode 1499

## 操作数

### uudecode

#### decode-pathname
uudecode 命令将解码后的文件存放在该位置的路径名。如果 decode-pathname 中包含不在可移植文件名字符集中的字符，则结果未定义。

#### source-file
要编码的文件路径名。

### uudecode

#### encoded-file
包含 uudecode 输出的文件路径名。

## 使用

有关 uudecode 和 uudecode 在遇到大于或等于 2 Gbytes (**31** 字节）的文件时的行为描述，请参阅 largefile(5)。

## 环境变量

参阅 environ(5) 获取以下影响 uudecode 和 uudecode 执行的环境变量描述：LC_CTYPE, LC_MESSAGES 和 NLPATH。

## 输出

标准输出是一个文本文件（使用当前区域的字符集编码），以以下行开头

```
begin&s@s\n, <mode>, decode_pathname
```

并以以下行结束

```
end\n
```

在两种情况下，这些行都没有前导或后续空白字符。
用于输出的算法通过拆分 begin 和 end 中的行，将六位间隔转换为四个字节组（octets），仅包含低六位的数据。通过为每个字节加上 0x20 的值将这些字节组转换为字符，使得每个字节都处于 0x20-0x5F 范围内。假设它表示一个可打印字符。每个字节都被翻译为当前区域所用编码的相应字符集。（例如，代表 A 的字节 0x41 在当前编码中被翻译为 A，如果它是 EBCDIC 则翻译为 0xC1。）

当两个字节组组合时，第一个字节组的低位左移并与第二个字节组右移后的高位组合。三个字节组 A, B, C 转换为四个字节组：

```
0x20 + ((A >> 2) & 0x3F)
0x20 + ((A << 4) & (B >> 4)) & 0x3F)
0x20 + ((B << 2) & (C >> 6) & 0x3F))
0x20 + ((C << 3) & 0x3F)
```

这些字节组被翻译为本地字符集。

## 1500

每行编码包含一个长度字符，等于要解码的字符数加上上述描述的 0x20 翻译为本地字符集的结果，随后是编码字符。每行可编码的字节组最大数量为 45。

## 退出状态

- * 0 成功完成。
- >0 发生错误。

## 属性

参阅 attributes(5) 获取以下属性的描述：

| 属性类型 | 属性值 |
| :--- | :--- |
| Availability | SUNWesu |

## 参见

mail(1), mailx(1), uucp(1C), uux(1C), attributes(5), largefile(5)

# uuglist — 打印可用服务等级列表

## 概要

/usr/bin/uuglist [-u]

## 描述

系统可以为 uucp 命令提供多个等级的服务。每个等级从 UUCP 系统获得不同的优先级。你可以使用 uuglist 命令显示系统上可用的服务等级列表，以便与 uucp(1C) 和 uux(1C) 的 -g 选项配合，如下例所示。

```
castle% uuglist -u
high
medium
castle%
```

## 选项

- * -u 列出 uucp 和 uux 命令的 -g 选项可以使用的服务等级。

## 文件

- /etc/uucp/Grades 包含服务等级列表。

# uulog, uuname 1501

## 属性

参阅 attributes(5) 获取以下属性的描述：

| 属性类型 | 属性值 |
| :--- | :--- |
| Availability | SUNWes |

## 参见

uucp(1C), uux(1C), attributes(5)

# uulog, uuname — UNIX 到 UNIX 的系统拷贝

## 概要

/usr/bin/uulog [-ssys] [-system] [-x]
/usr/bin/uuname [-c]

## 描述

参阅 uucp(1)。

# upick — 公共 UNIX 到 UNIX 的系统拷贝

## 概要

/usr/bin/upick [-system]

## 描述

参阅 uuto(1)。

# uustat — uucp 状态查询与作业控制

## 概要

/usr/bin/uustat [-m] [-p] [-q]
/usr/bin/uustat [-a] [-system]
/usr/bin/uustat [-c]

## 描述

uustat 在以下方面的功能：

- 显示 uucp 命令的状态。
* 提供远程系统性能，例如平均传输速率或平均等待时间。

## 1502

- * 提供 uucp 连接的通用、系统特定和用户特定状态。

**注意** 在用户发出 uucp 请求后，要移动、删除或拷贝到目录目录的文件最终因为找不到而失败。

## 选项

## 普通状态

以下选项获取 uucp 命令的状态或取消：

- -a 列出队列中的所有作业。
- -j 显示作业总数。你可以配合 -a 或 -s 使用此选项。
- -kjobid 杀死作业 ID 为 job 的 uucp 请求必须属于该用户，除非用户是超级用户或 uucp 管理员。超级用户或 uucp 管理员杀死作业，将向用户发送电子邮件。
- -m报告所有系统的可用性。
- -n 抑制所有标准输出，但保留标准错误。配合 -k 和 -r 使用此选项。
- -p 对锁文件中的所有进程 ID 执行 ps -flp。
- -q 列出每个系统的队列作业。如果系统存在状态文件，则报告其日期、时间和状态信息。此输出指示命令文件的数量（零表示调用系统，如果有工作要做的话）。日期和时间指的是与系统的上次交互，随后是交互状态。如果该系统的 c/x 文件数量旁边有括号，它是最旧文件的天数。重试标志表示下次可能调用的小时。计数是失败尝试次数。注意，对于具有中等数量未完成作业的系统，执行此命令可能需要30 秒或更长的实际时间。-q 产生的输出示例：

```
eagle 3C 04/07-11:07 NO DEVICES AVAILABLE
m3h3s 2C 04/07-10:42 SUCCESSFUL
```

