
# 高级 Bash 脚本指南

```bash
file_name=$(stat -cn "$FILENAME") # 显然相当于 "$FILENAME"
file_owner=$(stat -cU "$FILENAME")
file_size=$(stat -c "$FILENAME")
# 这比使用 sed 配合
# 'ls -l "$FILENAME' 要简单得多。
file_inode=$(stat -ci "$FILENAME")
file_type=$(stat -cf "$FILENAME")
file_access_rights=$(stat -cA "$FILENAME")
```

```bash
echo "File name: $file_name"
echo "File owner: $file_owner"
echo "File size: $file_size"
echo "File inode: $file_inode"
echo "File type: $file_type"
echo "File access rights: $file_access_rights"
```

```bash
exit 0
```

```bash
sh fileinfo2.sh
```

```
File name: testfile.txt
File owner: bozo
File size: 418
File inode: 1730378
File type: regular file
File access rights: -rw-rw-r-
```

### vmstat

显示虚拟内存统计信息。

```bash
vmstat
procs memory swap io system cpu
r b w swpd free buff cache si bo in cs us sy id
0 0 0 0 11040 2636 38952 0 0 33 7 271 88 8 3 8 9
```

### uptime

显示系统运行时间以及相关统计。

```
uptime
10:28pm up 1:57, 3 users, load average: 0.17, 0.34, 0.27
```

> 负载平均值为 1 表示系统可以立即处理进程。负载大于 1 意味着进程正在队列中。当负载平均值超过 3 时（在单核处理器上），系统性能会显著下降。

### hostname

列出系统名称。此命令设置 `/etc/rc.d` 启动脚本（`/etc/rc.d/rc.sysinit` 或类似）中的主机名。它等同于 `hostname -n`，并且是内部变量 `$HOSTNAME` 的对应项。

```bash
bash hostname
localhost.localdomain

bash echo $HOSTNAME
localhost.localdomain
```

类似于 `hostname` 命令的 `domainname`、`dnsdomainname`、`nisdomainname` 和 `ypdomainname` 命令。使用这些命令显示或设置系统 DNS 或 NIS/YP 域名。`hostname` 的各种选项也可以执行这些功能。

#### 第 17 章 系统与管理命令

### hostid

为宿主机回一个 32 位十六进制数字标识符。

```bash
bash$ hostid
7f0100
```

此命令始终为特定系统获取“唯一的”序列号。某些产品注册程序使用此数字来标记特定的用户许可。遗憾的是，`hostid` 只以十六进制形式返回机器网络地址，且部分字节经过转置。

典型非联网 Linux 机器的网络地址位于 `/etc/hosts` 中。

```bash
bash$ cat /etc/hosts
hostname.localdomain localhost
127.0.0.1
```

恰巧，在翻译地址 `127.0.0.1` 时，我们得到 `0F7E0170`，其精确的十六进制等值为 `007FE0100`。具有此相同 `hostid` 的 Linux 机器寥寥几个。

调用 `sar`（系统活动报告）可以提供非常详细的系统统计信息。Santa Cruz "Old" SCO 于 1999 年 6 月作为开源发布了 `sar`。

此命令不是 Linux 发行版的一部分，但可能是 Sebastian Godard 编写的 `sysstat` 工具包的一部分。

```bash
bash$ sar
Linux 2.4.9 (brooks.seringas.fr) 09/26/03
| | | %user | %nice | %system | %iowait | %idle |
| 10:30:00 | CPU | 2.21 | 10.90 | 65.48 | 0.00 | 21.41 |
| 10:40:00 | all | 2.21 | 0.00 | 72.36 | 0.00 | 24.28 |
| 10:50:00 | all | 3.36 | 0.00 | 72.36 | 0.00 | 24.28 |
| 11:00:00 | all | 1.12 | 0.00 | 80.77 | 0.00 | 18.11 |
| Average: | all | 2.23 | 3.63 | 72.87 | 0.00 | 21.27 |

LINUX RESTART
| | | %user | %nice | %system | %iowait | %idle |
| 15:00:00 | CPU | 8.59 | 2.40 | 17.47 | 0.00 | 71.54 |
| 15:10:00 | all | 4.07 | 1.00 | 11.95 | 0.00 | 82.98 |
| 15:20:00 | all | 0.79 | 2.94 | 7.56 | 0.00 | 88.71 |
| 15:30:00 | all | 6.33 | 1.70 | 14.71 | 0.00 | 77.26 |
| Average: | all | | | | |
```

### readelf

显示 elf 二进制文件的信息和统计数据。它是 `binutils` 包的一部分。

```bash
bash$ readelf -h /bin/bash
ELF Header:
Magic: 7f 45 46 46 01 01 00 00 00 00 00 00 00 00
Class: ELF32
Data: 2's complement, little endian
Version: 1 (current)
OS/ABI: UNIX - System V
ABI Version: 0
Type: EXEC (Executable file)
```

### size

`size` 命令给出二进制文件的大小。它是 `binutils` 包的一部分。

```bash
bash$ size /bin/bash
text: 94524 data: 2144 section: 22 allocated: 96668
```

# 高级 Bash 脚本指南

### 示例 17-6. pidof 帮助杀掉进程

```bash
#!/bin/bash
# kill-process.sh

NOPROC=2

process=xxxyyyyzz # 使用不存在的进程。
# 仅用于演示...
# ... 不想用这个脚本真正杀死任何实际的进程。
# 例如，如果你想用这个脚本注销网络连接，
#     process=$ppppid

t=$(pidof $process) # 查找 $process 的 pid (进程 ID)。
# 'kill' 命令需要 pid（无法通过程序名 'kill'）。

if [ -z "$t" ]; then # 如果进程不存在，'pidof' 将返回空值。
then
    echo "Process $process was not running"
    echo "Nothing killed."
    exit $NOPROC
fi

kill $t # 对于顽固的进程可以使用 kill -9。

# 这里需要一个检查，以查看进程是否允许自己被杀死。
# 也许可以再次执行 t=pidof $process 或者...

# 整个脚本可以被以下命令替换：
# kill $(pidof -x process_name)
# 或者
# killall process_name
# 但那样将没有这种指示意义。
```

`fuser` 可以识别（通过 PID）访问给定文件、一组文件或目录的进程。也可以通过 `-k` 选项调用，这会杀死这些进程。这对于系统安全具有重要的意义，特别是防止未授权的用户访问系统服务。

```
fuser -u /usr/bin/vim
usr/bin/vim: 3207e(bozo)
```

```
fuser -u /dev/null
/dev/null: 3009(bozo) 3010(bozo) 3197(bozo) 3199(bozo)
```

`fuser` 的一个重要应用是物理插入或移除存储媒体，如 CD ROM 磁盘或 USB 闪存。有时尝试挂载时会遇到“设备忙碌”（`device busy`）错误信息。这意味着某些用户和/或进程正在访问该设备。运行 `fuser -um /dev/device_name` 可以解开谜，你就可以杀死任何相关的进程。

```
fuser umount /mnt/usbdrive
umount: /mnt/usbdrive: device is busy
```

#### 第 17 章 系统与管理命令

# 高级 Bash 脚本指南

```bash
bash$ fuser -um /mnt/usbdrive
/mnt/usbdrive:      1772c(bozo)

bash$ kill -9 1772
bash$ umount /mnt/usbdrive
```

使用 `-n` 选项调用 `fuser` 命令可以识别访问端口的进程。它在与 `nmap` 配合时特别有用。

```
root# nmap localhost .localdomain
PORT STATE SERVICE
25/tcp  open    smtp

root# fuser -un tcp 25
25/tcp:               2095(root)

root# ps ax | grep 2095 | grep -v grep
2095 ?      Ss       0:00 sendmail: accepting connections
```

### cron

程序调度器，执行诸如清理和删除日志文件以及更新数据库等任务。这是 `at` 的守护版本（每个用户可能都有自己的 `crontab` 文件，可以使用 `crontab` 命令进行更改）。它作为守护进程运行，并执行 `/etc/crontab` 中的条目。

-   Linux Linux 版本的 `crond`，Matthew Dillon 的 `cron`。

# 进程控制与启动

## init

`init` 命令是所有进程的父进程。在启动的最后一步，`init` 从 `/etc/inittab` 确定系统的运行级别（`runlevel`）。通过其别名 `telinit` 调用，且仅限 `root` 调用。

## telinit

与 `init` 关联，这是更改系统运行级别的方法，通常用于维护或紧急文件系统。由 `root` 调用。此命令可能是危险的——在使用之前请务必确定。

`runlevel` 显示当前和上一次的运行级别，即系统是已停止（运行级别 0）、单用户模式（1）、多用户模式（2 或 3）、Windows 模式（5）还是正在重启（6）。该命令访问 `/var/run/utmp` 文件。

## halt, shutdown

设置为用于关闭系统的命令，通常在关机之前。

-   在 Linux 发行版中，`halt` 命令具有 755 权限，因此非 `root` 用户也可以调用。在终端或脚本中粗率地执行 `halt` 可能会关闭系统！

## service

启动或停止系统服务。`/etc/init.d` 和 `/etc/rc.d` 中的启动脚本使用此命令在启动时启动服务。

| `root# /sbin/service iptables stop` | [ OK ] |
|---|---|
| Flushing firewall rules: Setting chains to policy ACCEPT; filter | [ OK ] |
| Unloading iptables modules: | [ OK ] |

# 网络

## nmap

`nmap` 映射器和端口扫描器。此命令扫描服务器以定位开放端口以及与端口相关的服务。它还可以报告有关数据过滤器和防火墙的信息。这是一个防止网络黑客攻击的重要安全工具。

```bash
#!/bin/bash
SERVER=$HOST # localhost.localdomain (127.0.0.1)
PORT_NUMBER=25 # SMTP 端口。

nmap $SERVER | grep -w "$PORT_NUMBER" # 特定端口是否开放？
grep -w 仅匹配整个单词，
例如，它不会匹配端口 1025。

exit 0
# 25/tcp open smtp
```

网络接口配置和调优工具。

## ifconfig

```bash
bash$ ifconfig -a
lo LinkEnc:Loopback
 inet addr:127.0.0.1 Mask:255.0.0.0
 UP LOOPBACK RUNNING MTU:16436 Metric:1
 RX packets:10 errors:0 dropped:0 overflows:0 frame:0
 TX packets:10 errors:0 dropped:0 overflows:0 carrier:0 txlen:0
 RX bytes:700 (700.0 b) TX bytes:700 (700.0 b)
```

`ifconfig` 命令最常用于启动时在 `init.d/network` 中设置接口，或在重启时关闭。

```bash
# 取自 /etc/rc.d/init.d/network 的代码片段
# 检查网络是否启动。
[ $NETWORKING = "no" ] && exit 0

for i in $interfaces; do
    ifconfig -q
```

# 高级 Bash 脚本指南

转储 `bozoville` 和 `caduceus` 之间的 IP 数据包流量：

```bash
tcpdump ip host bozoville and caduceus
```

当然，`tcpdump` 的输出可以使用之前讨论过的某些文本处理工具进行解析。

# 文件系统

## mount

挂载文件系统，通常挂载在外部设备上，如软磁盘或 CD-ROM。文件 `/etc/fstab` 提供了可用文件系统、分区和设备的方便列表，包括可能被自动或手动挂载的选项。`/etc/mtab` 文件显示当前挂载的文件系统和分区（包括虚拟文件系统，例如 `/proc/`）。

`mount -a` 挂载 `/etc/fstab` 中列出的所有文件系统和分区，但带有 `noauto` 选项的除外。在启动时，`/etc/rc.d` 中的启动脚本（`rc.sysinit` 或类似文件）会被调用以获取挂载所有内容。

```bash
mount -t iso9660 /dev/cdrom /mnt/cdrom
# 挂载 CD-ROM。ISO 9660 是一种标准的 CD 文件系统。
/mnt/cdrom
# 如果 /mnt/cdrom 列在 /etc/fstab 中，这是一个快捷方式
```

多功能的 `mount` 命令甚至可以将普通文件挂载到块设备上，该文件将像块设备一样运行。`mount` 通过将文件系统与回环设备（loopback device）关联来实现。这种方法的应用是在将其刻录到 CDR 之前挂载并检查 ISO9660 文件系统镜像。

### 示例 17-7 检查 CD 镜像

```bash
# 作为 root...
mkdir /mnt/cdtest # 准备挂载点，如果还没有的话。
mount -r iso9660 -o loop cd-image.iso /mnt/cdtest # 挂载镜像。
# -o loop 选项等同于 "/dev/loop0"
cd /mnt/cdtest # 现在，检查镜像。
# 列出目录树中的文件。
ls -alR #以此类推。
```

## umount

卸载已挂载的文件系统。在移除之前挂载的软磁盘或 CD-ROM 磁盘之前，必须卸载该设备，否则可能会发生文件系统损坏。

```bash
umount /mnt/cdrom
# 现在你可以按下弹出键并安全地取出磁盘了。
```

> `automount` 工具如果安装正确，可以在访问或移除时自动挂载和卸载软磁盘或 CD-ROM 磁盘。然而，在具有可更换软磁盘和光驱驱动器的“多盘”笔记本电脑上，这会导致问题。

## gnome-mount

第 17 章 系统与管理命令

339

较新的 Linux 发行版已弃用了 `mount` 和 `umount`。其继任者是命令行挂载可移动存储设备的 `gnome-mount`。它可以接受 `-d` 选项通过其在 `/dev` 中的列表来挂载设备文件。

例如，挂载 USB 闪存：

```bash
bash$ gnome-mount -d /dev/sda1
gnome-mount 0.4
```

```bash
bash$ df
./dev/sda1    63584 12034 51550 19% /media/disk
```

`sync` 强制立即将所有更新数据从缓冲区写入硬盘（将驱动器与缓冲区同步）。虽然不是严格必要的，但 `sync` 能够确保系统管理员或用户刚刚更改的数据在突然断电时不会丢失。在过去，在重启之前执行 `sync; sync`（执行两次以确保万无一失）是一种非常有用的预防措施。

有时，你可能需要强制立即刷新缓冲区，例如在安全删除文件时（参见示例 16-61）或指示灯开始闪烁时。

`losetup` 用于设置和配置回环设备。

### 示例 17-8 在文件中创建文件系统
