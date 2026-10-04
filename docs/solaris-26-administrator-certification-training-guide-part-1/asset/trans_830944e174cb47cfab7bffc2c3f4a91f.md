
当程序执行时，系统会响应

- 看见 spot 吃
- 看见 spot 跑
- 看见 spot 跳
- 看见 spot 玩

如果你想交互式输入数据，可以添加 shell 特殊命令 read：

```
echo Hello- What\'s your name\?
read name
for i in $name
do
  echo $i
done
```

执行程序时，用户会被要求输入单词列表。注意反斜杠 (\) 的使用，这样 ' 和 ? 就会被原样处理，而不是用作特殊字符。

## While 循环

另一种循环是 while 循环。while 循环会持续重复执行一组命令，直到满足某个条件。while 循环的语法是

```
while condition-list
do commands
done
```

首先执行 condition-list。如果它返回 true 的退出状态，则执行 do 列表并从头开始重新操作。如果 condition-list 返回 false 的退出状态，则条件完成。以下示例说明了 while 循环。程序检查文件 /tmp/errlog 是否存在。如果文件不存在，程序退出循环。如果文件存在，程序打印一条消息并每 5 秒再次运行，直到文件被删除。

```
while [ -f /tmp/errlog ]
  do echo The file is still there ; sleep 5
done
```

注。特殊命令 sleep 5 指示系统在再次运行前等待 5 秒。

## Until 循环

until 循环是 while 语句的变体。正如 while 语句只要 condition-list 返回 true 值就重复执行，until 语句则重复执行直到 condition-list 返回 false 值。以下示例每 5 秒继续显示一条消息，直到文件被创建。

```
until [ -f /tmp/errlog ]
do echo the file is missing; sleep 5
done
```

while 和 until 等条件结构由 shell 执行，就像它们是一个单一命令一样。整个结构在执行任何部分之前都会被 shell 扫描。

## Shell 函数

任何好的编程语言都提供对函数的支持。函数是一组语句的集合，作为一个整体执行。这些集合的执行方式与“regular”命令一样，用于执行经常需要的任务。函数的一个优点是它存储在计算机的主内存中，因此执行速度比必须从磁盘检索的脚本快得多。当前版本的 Bourne shell 支持 shell 函数；旧版本的 Bourne shell 不支持。shell 函数的语法如下：

```
name()
{
command-list
}
```

上述命令语法定义了一个名为“name”的函数。函数体是 { 和 } 之间的 command-list。每当 name 被指定为命令的名称时，就会执行此列表。例如，在命令提示符下，输入

```
hello()
{
echo hello there
}
```

该函数名为“hello”，可以通过输入 hello 执行。函数的输出是 hello there。函数的退出状态是其主体中执行的最后一个命令的退出状态。

使用脚本和 shell 程序构建自己的命令是协助系统管理的强大而灵活的工具。常规任务可以简化并自动化，以节省您的时间，让您处理更 demanding 的任务。Shell 编程是所有 UNIX 系统管理员必须具备的技能，也是成为熟练 UNIX 用户的关键之一。

## 章节

## 9

## LP 打印服务

本章的测试目标如下：

- 了解 BSD 和 SystemV 打印系统之间的区别
- 了解 Solaris LP 打印服务
- 描述打印客户端和打印服务器
- 了解本地打印和远程打印之间的区别
- 描述 terminfo 数据库
- 了解如何使用 Admintool 创建、配置和修改打印机

打印机是任何计算机系统的标准外设。添加到新系统的第一个设备之一将是打印机。Solaris 操作系统的多用户特性意味着 Solaris 打印机软件比单用户操作系统的更复杂。这意味着向 Solaris 系统添加打印机不仅仅是即插即用。本章描述了将打印机连接到 Solaris 系统的所有方面。它描述了如何在操作系统中设置打印机以及安装后如何管理打印队列。

## UNIX 打印服务

设置 Solaris 打印机涉及设置硬件：打印机和打印机端口。此外，系统管理员需要验证是否有至少 8MB 的磁盘空间可用于 /var/spool/lp。打印文件将被发送到此位置以准备打印。其他配置文件将被创建，但 Solaris 操作系统会为您处理这一部分。当设置打印机时，Solaris 操作系统会根据需要对系统中的 /etc/printers.conf 和 /etc/lp 目录进行适当的更改。

## 打印排队程序

Spool 是 simultaneous peripheral operations online 的缩写。排队程序也称为队列。用户在想要打印某物时执行打印排队程序 lp。然后打印排队程序将用户想要打印的内容放入预定义的 /var/spool/lp 打印排队目录中。

排队空间是用于存储和处理打印队列中请求所占用的磁盘空间。/var 目录的大小取决于磁盘的大小和磁盘的分区方式。如果 /var 没有作为单独分区创建，/var 目录将使用部分根分区空间，而根分区空间可能相当小。一个大的排队目录可能消耗 600MB 的磁盘空间。查看可指定为打印服务器的系统上可用磁盘的大小和分区情况。

连接打印机时，首先仔细评估用户的打印需求和使用模式。如果用户通常只打印不需要复杂格式要求的简短 ASCII 文件，则分配给 /var 20 到 25MB 磁盘空间的打印服务器可能就足够了。然而，如果许多用户正在打印冗长的 PostScript 文件，他们会相当频繁地填满排队空间。当 /var 填满且用户无法将作业排队打印时，工作流程会被中断。/var 的大小在操作系统加载和磁盘分区时设置。

对于 SunOS 用户，SVR4 lp 程序等同于 BSD lpr 打印程序。在 SunOS 中，打印排队程序位于 /usr/spool。当 Sun 从 SunOS（基于 BSD UNIX）切换到 Solaris（基于 SVR4 UNIX）时，BSD 和 SVR4 之间的打印系统差异很大。在本章中，我将对可能熟悉该打印系统的系统管理员提及 BSD 打印系统。BSD 打印协议是行业标准。它被广泛使用并在不同制造商的各种系统之间提供兼容性。对于同时使用 BSD 和 SVR4 UNIX 的站点，Sun 在 Solaris 中为两种打印系统提供了兼容性。

## 打印守护进程

lp 进程是 SVR4 UNIX 中负责打印的 UNIX 实用程序。lp 打印守护进程由 lpsched 启动，是负责从排队目录获取输出并将其发送到正确打印机的 UNIX 进程。再次说明，对于 SunOS 用户，lp 等同于 BSD UNIX 中的 lpd。

可以使用多种方法在 Solaris 系统上定义打印机。表 9-1 描述了 Solaris 用于添加打印机的工具。

**表 9-1 Solaris 打印机实用程序**

| 实用程序 | 描述 |
|---|---|
| SunSoft Print Client Software | 一个接口，以前仅在 Solstice AdminSuite 管理工具集中可用，现在作为标准 Solaris 分发软件的一部分提供，用于设置打印客户端。 |
| Admintool | 用于在本地系统上创建、修改和删除打印机的图形用户界面。这是为新手用户添加打印机的推荐方法。 |
| Solstice AdminSuite | 用于在名称服务环境中管理打印机的图形用户界面 Print Manager 界面，仅在 Solaris 2.6 服务器软件发行版中可用。 |
| LP Print Service Commands | 用于设置和管理打印机的命令行实用程序。这些命令提供完整功能；Admintool 和 AdminSuite 包在高级任务方面 somewhat 受限。 |

本章描述了如何使用 Admintool GUI 或从命令行设置本地打印机、设置对远程打印机的访问以及执行一些打印机管理任务。系统管理员设置打印服务、向服务器添加打印机或从打印客户端添加对打印服务器上远程打印机的访问的大多数需求应由 Admintool 满足。从命令行设置打印机可能是一项非常复杂的任务。在继续研究该过程的更复杂部分——配置软件之前，我们将研究将打印机连接到 Solaris 系统所涉及的硬件问题。

## 设置硬件

将打印机连接到 UNIX 系统不是任何人的最爱活动，因为它可能很快变得耗时。市场上有许多打印机，每种都有略微不同的接口。将打印机本地连接到 Sun 系统时，您有三种选择之一：
