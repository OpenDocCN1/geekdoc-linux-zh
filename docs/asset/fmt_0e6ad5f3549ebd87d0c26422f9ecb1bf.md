
我们知道 `VERSIONID` 宏除了持有自定义版本控制信息外没有其他作用。我们也知道 `OSTYPE` 宏和两个 `MAILER` 宏是运行必需的。这使我们猜测移除 `DOMAIN` 宏是解决问题的开始。因此，在第 4 章中，我们创建一个简单的 `m4` 配置文件，用它生成与 `Sendmail 8.11` 兼容的 `sendmail.cf` 文件。它生效了，并让 `Sendmail` 运行了起来。

有时，基于猜测的快速解决方案是你所拥有的。当你有空闲时，你会回到这个问题上，找出为什么你的猜测是有效的，并确定是否有更好的长期解决方案。我们需要更多关于 `generic-linux.mc` 文件调用的宏源，以便：

*   发现简单更改是如何解决我们的问题的
*   看看是否有更好的方法解决我们的问题
*   发现由于我们的粗略方案丢失了哪些功能
*   了解更多关于配置 `Sendmail` 的知识

# 通用 Linux 配置 109

`generic-linux.mc` 文件调用的第一个源文件意料之中，是 `linux.m4` `OSTYPE` 文件。必须分析 `linux.m4` 文件的内容才能完全理解通用的 `Linux Sendmail` 配置。

## Linux OSTYPE 文件

`OSTYPE` 文件包含特定于操作系统的配置值。运行 `Sendmail` 的不同操作系统之间最大的配置差异在于文件的位置。定义路径模式的变量通常存储在 `OSTYPE` 文件中。由于该文件专门针对 `Linux` 操作系统，而这本书是关于在 `Linux` 上运行 `Sendmail` 的，让我们仔细观察一下 `OSTYPE` 文件。

`OSTYPE(linux)` 命令为 `ostype` 目录加载一个名为 `linux.m4` 的文件。列表 5.2 显示了该 `OSTYPE` 文件的内容：

**列表 5.2 的 linux.m4 OSTYPE 文件**

```
[craig$] cat ../ostype/linux.m4

divert(-1)

#
# Copyright (c) 1998, 1999 Sendmail, Inc. and its suppliers.
#   All rights reserved.
# Copyright (c) 1983 Eric P. Allman. All rights reserved.
# Copyright (c) 1988, 1993
#   The Regents of the University of California. All rights reserved.
#
# By using this file, you agree to the terms and conditions set
# forth in the LICENSE file which can be found at the top level of
# the sendmail distribution.
#
divert(0)

VERSIONID($Id: linux.m4,v 8.11.16.1 2000/05/09 18:48:58 ghapiiro
   Exp($')

define(`CONFEBINDIR', `/usr/sbin`)

ndef(`PROCMAIL_MAILER_PATH', `,
   define(`PROCMAIL_MAILER_PATH', `/usr/bin/procmail`))

FEATURE(`local_procmail`))
```

该文件以版权声明开头。版权声明被 `divert(-1)` 语句和 `divert(0)` 语句括围，因此被视为注释并可以安全地忽略。`VERSIONID` 宏也可以忽略。

![](img/9639113aa446fb8976cb3d377f7aafdd_132_0.png)

> **注意**：在本章的其余部分，为了减小列表尺寸，不会打印文件开头的版权声明，但你应该意识到它们是存在的。

文件中第一个真正的配置命令是 `define` 语句，它为 `CONFEBINDIR` 参数分配了一个值。该参数存储存放可执行二进制文件的目录路径。`Sendmail 8.11` 的 `CONFBINDIR` 的默认值是 `/usr/libexec`。此 `define` 将设置更改为 `/usr/sbin`。这两个目录在 `Linux` 系统上都存在，但 `/usr/sbin` 目录是更常用于存放系统二进制文件的目录，在这种情况下它是正确的。`CONFBINDIR` 路径用于定位 `smr` 邮件器（mailer），它在 `Linux` 系统上经常被用作程序邮件器（prog mailer）（第 12 章“`Sendmail` 安全”描述了使用 `smr` 邮件器的优势）。在我们的 `Linux` 系统上执行几个快速命令可以证明 `CONFBINDIR` 的正确值是 `/usr/sbin`：

```
[craig$] ls /usr/libexec/smrsh
ls: /usr/libexec: No file or directory
[craig$] ls /usr/sbin/smrsh
/usr/sbin/smrsh
```

第二个配置命令也是一个 `define`。这个稍微复杂一点。该 `define` 包含在 `ifdef` 内部。`ifdef` 与配置 `Sendmail` 无关。它是一个内置的 `m` 条件命令，用于检查变量是否已经被设置了值。`ifdef` 命令有三个字段：

*   正在测试的变量名
*   如果变量已设置，则要执行的操作
*   如果变量未设置，则要执行的操作

在列表 5.2 中，`ifdef` 测试变量 `PROCMAIL_MAILER_PATH`。如果该变量已经定义定义，则什么都不做。我们知道这一点的依据是 `ifdef` 的第二个字段是空的——注意紧挨着的两个逗号（`,,`）。如果变量未设置，则执行在 `ifdef` 第三个字段中包含的 `define`。这正是我们的示例系统上发生的情况，因为我们没有在宏配置文件中为 `PROCMAIL_MAILER_PATH` 分配任何值。

`define` 为变量 `PROCMAIL_MAILER_PATH` 分配路径值 `/usr/bin/procmail`。这覆盖了 `Sendmail` 对 `PROCMAIL_MAILER_PATH` 的默认值，即 `/usr/local/bin/procmail`。快速 `ls` 可以显示新值对于我们的示例系统是正确的：

```
[craig]$ ls -l /usr/bin/procmail
-rwxr-xr-x 1 root root 68276 Aug 10 1999 /usr/bin/procmail
```
