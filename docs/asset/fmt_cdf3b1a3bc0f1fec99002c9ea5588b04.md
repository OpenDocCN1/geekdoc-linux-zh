
# 第 2 章 软件组件

## 操作系统配置

作为管理员，你可能需要更新许多 PC 配置项。在 Windows 中，你可能需要向注册表中创建项，注册表是一个包含配置项的层次级数据库。

```text
PS C:\windows\system32\drivers\etc> 
Copyright (2003-2009) Microsoft Corp.
This is a sample HOST file used by Microsoft TCP/IP for windows.
此文件包含 IP 地址到主机名的映射。每个条目单独占一行表示一个主机；IP 地址应放在第一列，随后是相应的主机名。
地址和主机名之间至少有一个空格。
# 此外，注释（例如这些注释）可以插入在由 "#" 符号表示的机器名称后的行中。
# 例如：
102.54.94.97                # source server
38.63.10                    x.acme.com       # x client host
localhost name resolution is handled within DNS itself.
127.0.0.1                   localhost
::1                         localhost
C:\windows\system32\drivers\etc>
```

图 2-12 使用 Windows `type` 命令列出的文本文件

来源：Microsoft Windows 10/PowerShell

```text
root@CentOS7:~ -
File Edit View Search Terminal Help
[root@CentOS7 ~]# cat /boot/grub2/grub.cfg
#
# 不要编辑此文件
#
# 它是由 grub2-mkconfig 使用来自 /etc/grub.d 的模板 
# 以及来自 /etc/default/grub 的设置自动生成的。
### BEGIN BEGIN /etc/grub.d/00_header ###
set page=1

if [ -s $prefix/grubenv ]; then
  load_env
fi
if [ "${${entry}" ]; then
  set default="${entry}"
  set next_entry
  save_env_next_entry
  set boot_once=true
else
  set default="${saved_entry}"
fi

if [ "${feature_menu_id}" = xy ]; then
  menu_id_option="--"
else
  menu_id_option=""
fi

export menu_id_option
if [ "${prev_saved_entry}" ]; then
```

**图 2-13** 使用 `cat` 命令列出的文本文件

来源：Red Hat CentOS 7/Terminal

CentOS 7 中控制计算机系统的大多数配置文件以文本文件的形式存储。

### Windows 10 配置注册表编辑器

`Registryedit` 是一种特殊的实用程序，允许系统管理员编辑注册表项（参见图 2-14）。微软在 Windows 中使用注册表存储大量对 PC 正常运行至关重要的信息。你需要接触注册表，但不要尝试以任何方式对其编辑。

与 Windows 10 那样使用注册表不同，CentOS 7 将大多数配置设置文件维护在 `/etc` 目录下。如有必要，可以使用 `Vim` 文本编辑器编辑这些文本文件。你将在第 9 章学习该编辑器。

## 系统实用程序

| 名称 | 类型 | 数据 |
| --- | --- | --- |
| HKEY_CLASSES_ROOT | REG_SZ | (未设置值) |
| HKEY_CURRENT_USER | REG_DWORD | 00000003 (3) |
| HKEY_LOCAL_MACHINE | REG_DWORD | 000000541 (1345) |
| 00000000 | REG_BINARY | 00 00 00 00 00 00 00 00 00 00 00 00 |
| HARDWARE | REG_DWORD | 00 00 00 00 00 02 00 00 00 00 00 00 00 00 00 00 |
| DESCRIPTION | REG_SZ | AT/COMPATIBLE |
| System | REG_DWORD | 00000000 (0) |
| DESKTOP | REG_MULTI_SZ | VBOX - 1 |
| KeyboardClass | REG_MULTI_SZ | Sun VirtualBox Version 3.2.6 V |
| 2-1 |

图 2-14 使用 Regedit 显示的注册表项

来源：Microsoft Windows 10/Regedit

在 Windows 10 中，你可以使用任务管理器查看系统性能的有用信息；在 CentOS 7 中，你使用系统监控器。

对于系统管理员来说，最重要的问题是“我需要做什么？”一旦回答了这个问题，使用任务管理器或系统监视器就变得了。

### Windows 任务管理器

你使用任务管理器来监控计算机上运行的应用程序和进程。例如，在使用任务管理器时，你可以选择性地停止挂起的应用程序或进程以解决困境。你可以通过以下方式之一启动任务管理器：

- 按 `Ctrl+Shift+Esc`。
- 右键点击任务栏上的空白区域，从菜单中点击任务管理器。

你可以使用图 2-17 所示的选项卡来控制应用程序和进程，并查看系统和网络性能。后续章节将讨论这些许多选项卡。

#### 进程选项卡

你可以使用进程选项卡（见图 2-17）查看正在运行的应用程序名称以及计算机上运行的后台进程。该选项卡显示了进程（CPU）、内存、磁盘和网络的使用统计数据。然后你可以利用这些信息通过确定哪些程序正在使用最多资源（如处理器或内存）来排排除故障。CPU 值异常高的程序可能已经挂起。内存占用极大的程序可能存在内存泄漏——即进程的内存占用无限制增长。要停止进程，选择该程序并点击“结束任务”按钮。在该上，你可以通过点击列名对任何数据列进行排序。

通过结束进程可能会导致你的计算机不稳定或丢失内存中的宝贵数据！请小心。

![](img/290e46d5832f20e3707f4841e4e6d75a_87_0.png)

**图 2-17** Windows 任务器的进程选项卡

来源：Microsoft Windows 10 任务管理器

#### 性能选项卡

通过性能选项卡，你可以快速查看计算机对 CPU、内存、磁盘和网络资源的使用情况。选择每个资源查看详细信息。高 CPU 使用率（持续超过 90%）表示处理器速度不足。分页文件活动率高表示计算机需要额外的 RAM。要访问更详细的信息，点击“打开资源监视器”按钮。

![](img/290e46d5832f20e3707f4841e4e6d75a_88_0.png)

**图 2-18** Windows 任务器的性能选项卡

来源：Microsoft Windows 10/任务管理器

![](img/290e46d5832f20e3707f4841e4e6d75a_89_0.png)

**图 2-19** Windows 任务器的应用历史选项卡

来源：Microsoft Windows 10/任务管理器

#### 应用历史

你可以使用图 2-19 所示的应用历史选项卡来查看计算机应用程序利用率的历史记录。

#### Windows 资源监视器

你可以点击性能选项卡上的“打开资源监视器”按钮来监控四种关键资源的使用情况：CPU、硬盘、网络和内存。资源监视器会自动打开到“概述”选项卡。图 2-20 显示了资源使用的概览。此外，右侧会出现四个图表；点击四个箭头中的一个可以显示更详细的信息。点击 CPU、内存、磁盘或网络选项卡，可以获取每个组件的附加信息和统计数据。

![](img/290e46d5832f20e3707f4841e4e6d75a_90_0.png)

图 2-20 显示 CPU 详情资源监视器

来源：Microsoft Windows 10/任务管理器

### 活动 2-3：使用 Windows 10 任务管理器

所需时间：15 分钟

目标：使用 Windows 10 任务管理器查看 PC 的性能。

描述：在此活动中，你打开任务管理器的资源监视器，以检查 Windows 中运行的应用程序和进程。要快速查看 PC 的 CPU 性能，点击性能图表。在性能图表下方，你将检查若干关键计数器以确定所有进程和线程的活动对象（句柄）数量。你还将探索资源监视器以获取更多信息。如果你想查看系统任务和 PC 的性能，此活动非常有用。

1. 如果必要，使用活动 1-1 中的相应指令启动你的虚拟机。
2. 要启动任务管理器，右键点击任务栏，然后点击任务管理器。在屏幕底部，如果有必要，点击“更多详细信息”查看详细信息。
