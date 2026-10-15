
**列表 8-23** for test2.exp 示例，使用表达式为 `COUNT` 变量分配一个新计算的值。方括号确保了数学表达式在赋值给 `COUNT` 变量之前先进行评估。

## Expect 版本的函数

Expect 使用 `proc` 操作符而不是 `function` 关键字来支持函数。我们可以为函数定义参数。由于 shell 脚本的习惯，这里定义参数并不是必须的。让我们修改脚本，使用 `proc` 来增加 `COUNT` 变量，如列表 8-24 所示。

```bash
#!/usr/local/bin/expect -f

# 脚本 function_test.exp

############################

# 定义变量

############################

set COUNT 0

############################

# 定义函数

############################

proc increment_by_1 {
    set COUNT [expr $COUNT + 1]
    return "$COUNT"
}

############################

# 主程序

############################

while {$COUNT <= 10} {
    puts "\nCOUNT is currently at $COUNT"
    increment_by_1
}

puts ""
```

**列表 8-24** 函数示例

```expect
expect -exact "showplatform -v\r"
send -- "logout\r"
expect -exact logout\r
exit
expect eof
```

### 列表 8-25 `showplatform.exp` Expect 脚本

在列表 8-25 的 `showplatform.exp` Expect 脚本中，我们首先将第一个命令行参数赋予变量 `chassis`。接下来，我们通过将 `tout` 设置为 -1 来禁用超时。现在，我们启动了一个默认 shell 并 telnet 到 `$chassis`，它是刀片箱的主机名。

接着，我们等待用户名和密码提示，并发送正确的响应以登录机箱。现在我们可以执行 `showplatform -v` 命令并注销刀片箱。`showplatform.exp` 的示例输出如列表 8-26 所示。

```
wilma:> ./showplatform.exp sunchas
spawn /bin/sh
wilma:> telnet sunchas
Trying 192.168.1.142...
Connected to sunchas.
Escape character is '^'.
```

Sun Advanced Lights Out Manager for Blade Servers 1.2
Copyright 2003 Sun Microsystems, Inc. All Rights Reserved.
ALOM-B 1.2

```
username: prodmgr
password:
sunchas@>showplatform -v
```

| FRU | 状态 | 零件号 | 序列号 |
| --- | --- | --- | --- |
| S0 | 不存在 | *** | *** |
| S1 | 不存在 | *** | *** |
| S2 | 故障 | SF B100s | 540578 | 009897 |
| S3 | 正常 | SF B100s | 540579 | 013116 |
| S4 | 故障 | SF B100s | 540578 | 009973 |
| S5 | 故障 | SF B100s | 540578 | 010562 |
| S6 | 故障 | SF B100s | 540578 | 010111 |
| S7 | 故障 | SF B100s | 540579 | 010678 |
| S8 | 待机 | SF B100s | 540579 | 029965 |
| S9 | 正常 | SF B100s | 540579 | 029854 |
| S10 | 正常 | SF B100s | 540579 | 029698 |
| S11 | 不存在 | *** | *** |
| S12 | 不存在 | *** | *** |
| S13 | 不存在 | *** | *** |

**列表 8-26** `showplatform.exp` Expect 脚本运行示例

| S14 | 不存在 | *** | *** | *** |
| S15 | 不存在 | *** | *** | *** |
| SS00 | 正常 | SF B1600 SSC | 5405185 | 000470-0308000162 |
| SS00/SWT | | | | | |
| SS01 | 正常 | SF B1600 SSC | 5405185 | 000470-0047005951 |
| SS01/SWT | | | | | |
| PS00 | 正常 | SF B1600 PSU | 3001544 | 0017527-0324P02770 |
| PS01 | 正常 | SF B1600 PSU | 3001544 | 0017527-0324P02700 |
| CH | 正常 | SF B1600 | 5405082 | 001635 |
| 域状态 | MAC 地址 | 主机名 |
| S2 | OS 运行中 | 00:03:bb84:4c:d0 | sunblld2 |
| S3 | OS 运行中 | 00:03:bb8c:ea:bc0 | sunblld3 |
| S4 | OS 运行中 | 00:03:bb59:fe:e8 | sunblld4 |
| S5 | OS 运行中 | 00:03:bb84:33:62 | sunblld1 |
| S6 | OS 运行中 | 00:03:bb84:37:c2 | sunblld2 |
| S7 | OS 运行中 | 00:03:bb84:2e:80 | sunblld4 |
| S8 | 待机 | 00:03:bb44:4f:5c | sunbld1 |
| S9 | OS 运行中 | 00:03:bb34:42:1e | sunblld2 |
| S10 | OS 运行中 | 00:03:bb34:40:88 | sunblldd1 |
| SS00/SWT | | 00:03:bb34:42:1e | |
| SS00/SWT | | 00:03:bb34:40:88 | |
| SS00/SWT | | 00:03:bb84:3e:8 | |
| SS00/SWT | | 00:03:bb84:3e:80 | |

（注：由于原始文本中存在大量重复和乱码片段，上述译文已根据上下文逻辑进行了清理和整合，确保了核心技术内容的准确性。）

## 查找大文件和特定类型的文件

文件系统警报！我们都讨厌收到文件系统满的报警，尤其是在周五下班前，当时开发者正忙于赶截止日期。通常的罪魁祸首是一个或多个刚刚创建、编译或加载的大文件。“大文件”的定义取决于系统环境，但一个“大”文件就能迅速填满文件系统，特别是在大型数据库或开发环境中。为了找到快速填满文件系统的文件和或大文件，我们需要一个灵活的工具来搜索大于用户定义值的文件。当需要系统搜索时，`find` 命令就是你的朋友。

`find` 命令是系统中最灵活、强大的命令之一。在我们开始之前，我希望你有一份 `find` 命令的帮助页副本。你有两种方法可以保存 `find` 命令帮助页的副本。第一种方法使用纸（你知道的，在打印机里），第二种方法是节省很多棵树。要将 `find` 命令帮助页发送到特定的打印队列（换句话说，烧掉一些树），请输入以下命令：

```bash
man find | lp -d print_queue_name
```

如果你对保护地球感兴趣，可以通过执行以下命令来归档 `find` 命令帮助页：

```bash
man find | col -b >> find.txt
```
