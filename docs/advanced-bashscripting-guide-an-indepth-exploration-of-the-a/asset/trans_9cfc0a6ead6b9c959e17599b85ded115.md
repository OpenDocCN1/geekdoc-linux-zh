

## 高级 Bash 脚本指南

更改 ROOT 目录。通常命令是从 $PATH 中获取的，相对于 `/`（即默认根目录）。此命令会将根目录更改为另一个（同时也会更改工作目录）。这对于安全目的非常有用，例如当管理员希望限制用户（如使用 telnet）访问文件系统的安全部分时；它有时通过将用户限制在“chroot 监狱”中来实现限制。请注意，在执行 chroot 之后，系统二进制文件的执行路径将不再有效。

`chroot /opt` 会创建对 `/usr/bin` 的引用并转换为 `/opt/usr/bin`。同样，`chroot /aaa/bbb /bin/ls` 将限制未来的 `ls` 实例以 `/aaa/bbb` 为基础目录（这是通常的情况）。在用户的 `~/.bashrc` 中设置 `alias xx='chroot /aaa/bbb'` 可以有效限制其运行命令 "XX" 时可以操作的文件系统部分。

chroot 命令还用于从空软磁盘运行（chroot 到 `/dev/fd0`），或在从系统崩溃中恢复时作为 `l` 的选项。其他人使用从不同的文件系统进行安装（一个 rmp 选项）或从 CD-ROM 运行只读文件系统。仅以 root 身份调用，并谨慎使用。

![](img/1ce1edffaa36e4f698a85430e71c6d3b_221_0.png)

可能需要将系统文件复制到 chrooted 目录，在其中无法再依赖标准的 $PATH。

此实用程序是 procmail 软件包（www.procmail.org）的一部分。它会创建一个锁文件。

锁文件用于此类应用程序，例如保护系统邮件文件夹不被多个用户同时修改、指示调制解调器正在访问，以及显示 Netscape 实例正在使用其缓存。脚本通过检查进程创建的锁文件是否存在来检查该进程是否正在运行。请注意，如果脚本尝试创建一个已存在的锁文件，脚本可能会挂起。

通常，应用程序在 `/var/lock` 目录中创建并检查锁文件。脚本可以通过类似内容来测试锁文件是否存在。

```
appname=xyzip
# Application "xyzip" 创建了锁文件 "/var/lock/xyzip.lock"

if [ -e "/var/lock/$appname.lock ]
then
```

创建块或字符设备文件（在系统上安装新硬件时可能是必要的）。

自动删除在指定时间内未被访问的文件。通常由 `crond` 调用以删除过期的日志文件。

## MAKEDEV

用于创建设备文件的实用程序。必须以 root 身份运行，并在 `/dev` 目录下执行。

```
root# ./MAKEDEV
```

这是 `mknod` 的一种高级版本。

## 备份

dump, restore

`dump` 命令是一个精细文件系统备份工具，通常用于较大的安装和网络环境。[42]。它读取原始分区并以二进制格式写入备份文件。要备份的文件可以使用多种存储媒体，包括磁盘和磁带驱动器。`restore` 命令恢复用 `dump` 创建的备份。

## fdformat

在软磁盘上执行低级格式化。

## 系统资源

### ulimit

设置系统资源的上限。通常带有 `-f` 选项调用，该选项设置文件大小限制（`ulimit -f 1000` 将文件限制为最大 1MB）。`-t` 选项限制核心转储大小（`ulimit -c 0` 消除核心文件）。通常，`ulimit` 的值设置在 `/etc/profile` 和或 `~/.bash_profile` 中（见第 27 章）。

### umask

用户文件创建掩码。限制特定用户的默认文件属性。该用户创建的所有文件都使用由 umask 指定的属性。（（传递给 `umask` 的八进制值定义了禁用的文件权限）。当然，`umask 002` 确保新文件的权限最多为 755。通常做法是在 `/etc/profile` 和 `~/.bash_profile` 中设置 umask 值（见第 27 章）。

### rdev

获取或更改根设备、交换空间或视频模式。`rdev` 的功能已被 `lilo` 取代，但 `rdev` 仍用于设置内存磁盘。这是另一个危险命令。

## 模块

### lsmod

列出已安装的内核模块。

| 模块 | 大小 | 使用者 |
|---|---|---|
| autofs | 9456 | 2 (autoclean) |
| opli3 | 11376 | 0 |
| serial_cs | 5456 | 0 (unused) |
| sb | 34752 | 0 [sb] |
| uart401 | 6384 | 0 [opli3 sb uart401] |
| sound | 58368 | 0 [sound] |
| soundlow | 464 | 0 [sb, sound] |
| soundcore | 2800 | 2 [serial_cs] |
| ds | 6448 | 0 |
| i28365 | 22928 | 2 |
| pcmia_core | 45984 | 0 [serial_cs ds i28365] |

insmod

强制安装内核模块。必须以 root 身份调用。

rmmod

强制卸载内核模块。必须以 root 身份调用。

modprobe

模块加载器，通常在启动脚本中自动调用。

depmod

创建模块依赖文件，通常从启动脚本调用。

## 杂项

env

在设置或更改某些环境变量的情况下运行程序或 shell（而不更改整体系统环境）。`[varname=xxx]` 允许在脚本运行期间更改环境变量名称。在未指定选项的情况下，此命令会列出所有环境变量。

> 在 Bash 和其他 Bourne 衍生版本中，可以在单个命令的环境中设置变量。

```
var1=value var2=value2 commandXXX
#var1 和 $var2 仅在 'commandXXX' 的环境中设置
```

> 脚本的第一行（"sha-bang" 行）在 shell 或解释器路径未知时可以使用 env。

```bash
#!/usr/bin/env perl
print "This Perl script will
```

