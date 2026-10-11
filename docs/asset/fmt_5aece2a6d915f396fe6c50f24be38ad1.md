
另一个最初旨在替代 Linux 中 `man` 命令的工具是 GNU `info pages`。你可以通过输入 `info` 命令后跟目标命令的名称来访问此工具。`info` 命令会返回每个命令的易于阅读的描述，并包含指向其他信息页的链接（称为超链接）。今天，info 页和手册页（manual pages）都用于查找文档，因为手册页从 Linux 诞生之初一直被使用，在 UNIX 操作系统中已使用了二十多年。以下是使用 `info` 查找 `whoami` 命令信息的示例：

```
[root@server1 root]# info whoami
```

info 页是交互式显示的：

```
Next: groups invocation, Prev: logname invocation, Up: User information
```

## 第 2 章 Linux 安装与使用

### 20.3 'whoami': 打印有效用户 ID

============================

`whoami` 输出与当前有效用户 ID 相关的用户名。它等同于命令 `id -un`。

唯一的选项是 `--help` 和 `--version`。`注意常用选项：`

退出状态零表示成功，非零表示失败

```
------Info: (coreutils)whoami invocation, 14 lines -All------
Welcome to Info version 6.5. Type H for help, h for tutorial.
[root@server1 root]#
```

> 注意：在使用帮助（help）程序时，按 H 键可以显示描述 info 用法的帮助屏幕。与 man 命令一样，你可以使用 q 键退出。

某些命令没有手册页或 info 页。这些命令是内置在 BASH 壳本身中的函数。要查找这些命令的帮助信息，你需要使用 `help` 命令，如下所示：

```
[root@server1 root]# help echo
echo: echo [-neE] [arg ...]
将参数写入到标准输出。
```

在标准输出上用单个字符分隔并后换行符显示 ARGs。

- -n 不追加换行符

- -e 启用对后续反斜杠转义的解释

- -E 显式抑制对反斜杠转义的解释

`echo` 解析以下反斜杠转义字符：

\a 警报（铃声）

\b 退格

```
\c 抑制后续输出
\e 转义字符
\E 转义字符
\f 分页
\n 换行
\r 回车
\t 水平制表
\v 垂直制表
\\ 反斜杠
\nnn ASCII 码为 NNN 的字符（八进制）。NNN 可以是 0 到 3 位八进制数字
\xHH 值为 HH 的八位字符（十六进制）。HH 可以是一个或两个十六进制数字
```

退出状态：

除非发生写入错误，否则返回成功。

```
[root@server1]#
```

### 关闭 Linux 系统

由于操作系统处理从计算机内存到磁盘驱动器的数据，关闭计算机电源可能会导致用户和系统文件损坏。因此，在关闭计算机硬件组件电源之前，为操作系统做好关闭准备至关重要。要做到，你可以发布 `shutdown` 命令，该命令可以在一段时间后关闭或重启（重新启动）你的计算机。若要在 15 分钟后关闭系统，你可以输入：

```
[root@server1] # shutdown -P +15
```

这将产生类似下方的输出：

```
Shutdown scheduled for Wed 2019-09-17 15:51:48 EDT, use 'shutdown-c' to cancel.
```

在调度系统关机之前，最好告知当前登录系统的用户，他们可以提前保存工作并注销。你可以使用 `wall`（警告所有人）命令后跟发送给系统用户的消息：

```
[root@server1 root] # wall The system is shutting down in 15 min ensure that you save your work and log off before then.
```

若要在现在关闭系统，你可以输入：

```
[root@server1 root] # poweroff
```

## 第 2 章 Linux 安装与使用

`shutdown` 命令的其他示例及其描述见表 2-9。

### 表 2-9 停止和重启 Linux 操作系统的命令

| 命令 | 描述 |
| :--- | :--- |
| shutdown -P +4 | 在四分钟后关闭系统 |
| shutdown -H +4 | 在四分钟后停止操作系统的运行，但不会调用 BIOS 中的 ACPI 功能为计算机断电 |
| shutdown -r +4 | 在四分钟后重启系统 |
| shutdown -P now | 立即重启系统 |
| shutdown -c | 取消已调度的关机 |
| halt | 立即停止系统运行，但不会关闭电源 |
| poweroff | 立即关闭系统 |
| reboot | 立即重启系统 |

## 章节总结

- 在安装之前，你应该验证硬件要求和兼容性。

- 你可以通过从互联网下载 ISO 镜像来获取 Linux 安装介质，该镜像可以写入 DVD 或 USB 驱动器，或直接供虚拟化软件使用。

- 典型的 Linux 安装会提示用户提供信息，如语言、日期、时区、键盘布局、用户帐户和持久性存储配置。

- 用户必须登录终端并接收 shell 才能与 Linux 系统和内核进行交互。单个用户可以多次登录本地或跨网络的不同终端。

- 无论你使用哪种类型的终端（图形或命令行），你都可以在提示符处输入命令和参数来执行任务、获取帮助或关闭 Linux 系统。shell 是区分大小敏感的，并理解各种称为元字符的特殊字符，如果不需要它们的特殊含义，应对其进行保护。

### 关键术语

- 高级技术附件 (ATA)

- Btrfs (BTRFS)

- 基础输入输出系统 (BIOS)

- BIOS 启动分区

- ext2

- ext3

- ext4

- 扩展分区

- GUID 分区表 (GPT)

- 硬件兼容列表 (HCL)

- info 页

- 集成驱动器 (IDE)

- ISO 镜像

- 日志记录 (journaling)

- 现场介质

- 逻辑驱动器

- 逻辑卷管理器 (LVM)

- 手册页 (man pages)

- 主引导记录 (MBR)

- 元字符

- 命名空间

- 非易失性内存表达式 (NVME)

- 并行技术附件 (PATA)

- 主分区

- 冗余磁盘阵列 (RAID)

- 序列附件 (SATA)

- 串连接 SCSI (SAS)

- 小型计算机系统接口 (SCSI)

- 固态硬盘 (SSD)

- 交换内存

- UEFI 系统分区

- 统一扩展固件接口 (UEFI)

- 虚拟分配表 (FAT)

- 虚拟机

- 虚拟内存

- 虚拟化软件

- XFS

### 复习题

1. Linux 中默认的 shell 是什么的？

   a. SH

   b. Bash

   c. CSH

   d. BASH

2. 哪种等同于 man 命令的内容通常提供更易读的命令描述并包含指向其他信息的链接？

   a. who

   b. man help

   c. man desc

   d. info

3. 你可以使用哪个命令安全地立即关闭 Linux 系统？

   a. shutdown -c

   b. shutdown -r

   c. down

   d. halt

4. 哪个命令与 man -k 命令等同？

   a. find

   b. man

   c. apropos

   d. appropos

5. 下列哪项不是 Fedora 安装程序提示你提供的信息？

   a. 时区

   b. 安装目标

   c. 防火墙设置

   d. 安装语言

6. 通过命令行输入的 Linux 命令是对大小敏感的。对或错？

7. 哪个命令清空终端屏幕，删除之前显示的输出？

   a. erase

   b. clean

   c. blank

   d. clear

8. 当坐在运行 Linux 的电脑前时，按下哪个组合键可以打开图形终端？

   a. Ctrl+Alt+G

   b. Ctrl+Alt+F4

   c. Ctrl+Alt+F1

   d. Ctrl+7

9. 在虚拟机内安装 Linux，你可以指定包含 Linux 安装介质的 ISO 镜像路径，而无需先准备 DVD 或 USB 驱动器的 ISO 镜像。对或错？

10. 登录终端后，你会接收到一个称为 ___ 的用户界面。

    a. GUID

    b. shell

    c. 文本框

    d. 命令行屏幕

11. 用户直接向 Linux 操作系统的内核输入命令。对或错？

12. 如何保护元字符（例如 $ 字符）不被 shell 解释？

    a. 在其前面加 /

    b. 在其后面加 \

    c. 在其前面加 $
