
`echo "$* added to database"`

`exit 0`

`fi`

# 不是。但文件里有内容吗？

# 毕竟，这可能是我们第一次使用它。

`if [ -s $HONELIST ]; then`

`echo "No names in phone list yet!"`

`exit 1`

`else`

`grep -iq "$*" $HONELIST` # 静默搜索文件

`if [ $? -ne 0 ]; then`

# 我们找到了什么吗？

`echo "Sorry, that name was not found in phone list"`

`exit 1`

`else`

`grep -i "$*" $HONELIST`

`fi`

`fi`

`exit 0`

因此，如果你在当前目录下创建了名为 `phone` 文件，你可以从 shell 输入以下内容来尝试你的脚本：

```bash
chmod 755 phone
./phone "new"
```

`chmod` 命令使脚本变得可执行。`./phone` 命令从当前目录带有新选项运行。这会将 `phone` 作为名称和号码添加到数据库（`$HOME/.phone.txt`）。如果脚本运行正常，将其添加到你的 `PATH` 目录中（例如 `$HOME/bin`）。

# 一个简单的备份脚本

因为没有什么是永恒的，错误在所避免，所以在处理计算机数据时，备份是生活的常态。这个简单的脚本备份了 Fedora 或 RHEL 系统上所有用户家目录中的所有数据。

```bash
#!/bin/bash

# 一个简单的备份脚本

# 修改 TAPE 设备以匹配你的系统。

# 检查 /var/log/messages 以确定你的磁带设备。

# 你可能还需要向你的内核添加 scsi-tape 支持。

TAPE=/dev/rmt0

# 回位磁带设备

mt $TAPE

# 获取家目录列表

HOMES=$(grep /home /etc/passwd | cut -f6 -d:)

# 备份这些目录中的数据

tar cvf $TAPE $HOMES

# 回位并弹出磁带。

mt $TAPE
```

交叉引用：请查看第 13 章有关备份和恢复文件的详情以及获取 `mt` 命令（必须单独安装的 `tapeutils` 软件包的一部分）。

# 系统初始化

当你打开电脑时，在 Fedora 或 RHEL 启动之前会发生很多事情。以下是每次启动电脑运行 Fedora 或 RHEL 时发生的基本步骤：

1. **启动硬件** —— 根据计算机只读存储器（称为 BIOS）中的信息，你的计算机检查并启动硬件。这些信息中的某些部分告诉计算机哪些设备（软盘）。

2. **启动引导程序** —— 假设你安装了引导程序，BIOS 会检查可启动设备（软盘、CD、硬盘等）以查找可启动操作系统。

3. **启动内核** —— 假设你选择了 Fedora 或 RHEL，内核加载。内核挂载文件系统并将控制权交给 `init` 进程。

## 启动 init

从内核阶段（探测设备和加载驱动程序）到 `init` 的传输由以下行指示：

欢迎使用 Fedora
按 "I" 进入交互式启动

`init` 程序（`sysinit` 软件包的一部分）现在接管了控制权。`ps` 输出总是列出 init（所有进程的父进程）为 PID 1。它的操作由 initab 文件引导。

## initab 文件

示例显示 Fedora 提供的 initab 内容：

纯文本 initab 文件由多个冒号分隔的字段组成，格式如下：
`id:runlevels:action`

`id` 是一个唯一标识符，长度为四个字母字符，代表系统启动期间的特定操作。`runlevels` 包含运行该命令的运行级别列表。下一个字段代表 init 采取的操作类型（有效操作及其结果见表 12-3），最后一个字段是要执行的实际命令。

```bash
# initab
# 此文件描述了 init 如何设置系统。
0:wait:/sbin/shutdown -h
1:wait:/etc/init
2:wait:/etc/init
3:wait:/etc/init
4:wait:/etc/init
5:wait:/etc/init
6:wait:/etc/init
a:powerfail:/sbin/shutdown -f
b:powerrestored:/sbin/shutdown -c
c:powerkill:/sbin/shutdown -k
```
