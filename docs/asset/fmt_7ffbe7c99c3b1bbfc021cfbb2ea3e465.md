
```bash
#!/bin/bash
echo -e "This program copies a file to the /staff directory.\"
echo -e "Which file would you like to copy?-->\c"
read FILENAME
mkdir /staff || echo "The /staff directory could not be created."
cp -f $FILENAME && echo "$FILENAME was successfully copied to /staff"
```

### 16.
在命令提示符下，输入 `chmod u+x myscript3` 并按回车。接下，在命令提示符下输入 `./myscript3` 并按回车。当提示文件名时，输入 `/etc/hosts` 并按回车。`/staff` 目录创建成功了吗？为什么？`etc/hosts` 文件成功复制到 `/staff` 目录了吗？为什么？

### 17.
在命令提示符处输入 `./myscript3` 并按回车。当提示文件名时，输入 `/etc/initab` 并按回车。`/stuff` 目录是否成功创建？为什么或为什么？`/etc/initab` 文件是否成功复制到 `/stuff` 目录？为什么或为什么？

### 18.
输入 `exit` 并按回车退出你的 shell。

## 发现练习

### 1. 写出用于以下操作的命令：

- a. 创建别名 `mm`，仅显示已挂载且包含 `ext2` 文件系统的文件。
- b. 创建并导出一个变量 `NEWHOME`，其值等于 `HOME` 变量。
- c. 从 `/etc` 目录查找所有以 "host" 开头的文件，并将标准输出保存到名为 `file1` 的文件中，将标准错误保存到同一个文件中。
- d. 从 `set` 命令的输出中仅显示包含 "bash" 的文件。屏幕输出应按字母排序。
- e. 在冒号分隔的 `/etc/password` 文件中仅显示用户名（第一个字段），并将输出保存到当前目录下的 `users` 文件中。

### 2.
如果用户执行以下命令，会发生什么？

```
tr A </etc/hosts | sort -r | pr -d >/etc/hosts
```

解释输出结果。

### 3.
回想标准输出可以通过管道发送到另一个命令。根据本章提供的信息，你如何通过管道向以下命令发送标准错误？

`ls /etc/hosts | tr h H`

### 4. 写出一个测试语句，用于测试：

- a. 用户对 `/etc/hosts` 文件是否有读取权限。
- b. 用户对 `/etc` 目录是否有读取和执行权限。
- c. 变量 `$TEST` 的内容是否等于字符串 "success"。
- d. 变量 `$TEST` 的数值是否等于变量 `$RESULT` 的内容。
- e. 变量 `$TEST` 的内容是否等于字符串 "success" 且 `/etc/hosts` 文件是否存在。
- f. 变量 `$TEST` 的内容是否等于字符串 "success" 或变量 `$RESULT` 的内容。

### 5.
接下来所示的 `/root/.bash_profile` 文件。根据本章提供的信息，描述该文件每一行的作用。

```
## .bash_profile

## 获取别名和函数
if [ -f ~/.bashrc ]; then
    ~/.bashrc
fi

## 用户特定环境和启动程序

PATH=$PATH:$HOME/bin
BASH_ENV=$HOME/.bashrc
USERNAME="root"

export USERNAME BASH_ENV PATH
```

### 6.
写一个包含注释的 脚本。它应该执行以下任务：

- a. 显示当前登录用户列表。
- b. 显示系统主机名。
- c. 显示日期。
- d. 显示当前工作目录。
- e. 显示磁盘使用情况。
- f. 显示 BASH shell 的路径。

### 7.
写一个 脚本，提示用户输入 0 到 100 之间的分数。脚本应根据以下标准计算该分数对应的字母：

- 0-49 = F
- 50-59 = D
- 60-69 = C
- 70-79 = B
- 80-100 = A

# 第 9 章

# 系统初始化与 X Windows

完成本章后，你将能够：

- 总结启动 Linux 系统所需的后续步骤。
- 配置 LILO 和 GRUB 引导程序。
- 使用 LILO、GRUB 和 NTLOADER 实现 Linux 与 Windows 操作系统的双引导。
- 理解 init 进程如何在启动时将系统初始化为不同的级别。
- 配置系统在启动时启动进程。
- 解释主要 Linux GUI 组件的过程：X Windows、管理器和桌面环境。
- 列出 Linux 中常用的管理器和桌面环境。
- 使用各种 Linux 工具配置 X Windows 设置。

在本书前面，你在 Red Hat Fedora 安装期间为 Linux 内核安装了 GRUB 引导程序。在本章中，你将更详细地研究启动过程。你将探索引导程序的不同类型和配置，以及 Linux 系统与 Windows 操作系统的双引导过程。在本章后面，你将学习在内核加载后启动进程的程序，以及如何操作该程序来启动和停止新进程。最后，你将检查 Linux GUI 的组成部分，以及如何使用常用的 Linux 工具配置 GUI。

## 启动过程

当电脑启动时，主板上的 BIOS 执行电源自检（POST）。POST 之后，BIOS 检查主板上 CMOS 芯片中的配置，以搜索启动设备和要执行的操作系统。通常，电脑首先检查软盘以及电脑中带有磁盘的 CD-ROM 设备上的操作系统。这确保了从光盘或软盘启动操作系统可以在启动时发生。在检查了这两个设备后，电脑通常会检查第一块硬盘上的主引导记录（MBR）。这确保了从光盘或软盘启动操作系统可以在启动时发生。

# 引导程序 383

表 9-1 常用 `/etc/lilo.conf` 关键字（续）

| 关键字 | 描述 |
| --- | --- |
| `message=` | 指定包含图形化 LILO 屏幕文件的绝对路径，该屏幕可以代替提示符。在该图形界面上可以按 Ctrl+x 切换到 LILO 启动提示符。 |
| `timeout=` | 指定在加载默认操作系统内核之前等待用户插入等待秒数（以 1/10 秒为单位）。 |
| `default=` | 指定默认操作系统内核的标签（label）。 |
| `label=` | 指定赋予操作系统内核的友好名称。 |
| `boot=` | 指定 LILO 的安装位置。如果指定的设备在硬盘上，则 LILO 安装在分区的开头。如果指定的设备是磁盘，则 LILO 安装在设备设备的 MBR 上。 |
| `linear` | 指定 LILO 使用线性扇区寻址。 |
| `read-only` | 最初将 Linux 根文件系统挂载为只读，以减少运行系统设置期间可能出现的任何错误。 |
| `initrd=` | 指定用于启动时将模块加载到 Linux 内核的 ramdisk 镜像路径。 |
| `password=` | 指定启动 Linux 内核所需的密码。 |
| `append=` | 指定加载时传递给 Linux 内核的参数。 |
| `map=` | 指定包含 Linux 内核在硬盘上精确位置的文件。 |
| `install=` | 指定包含磁盘驱动物理布局的文件。 |
| `lba32` | 为具有超过 1024 个磁道的驱动器指定大寻址（32 位）。 |

通过在 `/etc/lilo.conf` 中的某些行前面加上 `#` 符号，可以将这些行注释掉。

![](img/9ee5f91f3446575a1e6ce62c54cae5d2_404_0.png)

`/etc/lilo.conf` 中的 `append=` 关键字非常用于在内核没有检测到正确系统信息时，在启动时手动将信息传递给 Linux 内核。请记住，系统会将检测到的硬件信息导出到 `/proc` 目录；查看 `/proc` 目录下的文件内容可以判断 Linux 内核是否正确检测了硬件。如果内核没有识别 `/proc/meminfo` 文件中的所有物理内存，你只需向 `/etc/lilo.conf` 添加一行 `append="mem=xxx"`，其中 `xxx` 是正确的兆字节（MB）内存量。此外，如果系统未能正确检测到硬盘，你可以在启动时将硬盘正确的磁道、磁头和扇区发送给内核；要这样做，请向 `/etc/lilo.conf` 添加行 `append="hdC,H,S"`，其中 `C`=磁道，`H`=磁头，`S`=扇区。

几乎任何硬件信息都可以通过 `append=` 关键字传递给内核。信息的格式取决于涉及的硬件类型。

![](img/9ee5f91f3446575a1e6ce62c54cae5d2_404_1.png)

# 第 9 章 系统初始化与 X Windows

如果你更改了 `/etc/lilo.conf` 文件，则必须使用 `/etc/lilo.conf` 中的新信息重新安装 LILO，更改才能生效。要做到这一点，你可以使用 `lilo` 命令：
