

# 列表 7-4：使用关机与重启脚本

```bash
#! /bin/sh
#
# rc.6       此文件由 init 在进入 runlevel 0 (halt) 或 runlevel 6 (reboot) 时执行。它会终止所有进程，卸载文件系统，然后执行停机或重启。
#
# 版本:  @(#)/etc/rc.d/rc.6    1.50    1994-01-15
#
# 作者:   Miquel van Smoorenburg <miquels@drinkel.nl.mugnet.org>
# 修改者: Patrick J. Volkerding, <volkerdi@ftp.cdrom.com>
#
# 设置路径。
PATH=/sbin:/etc:/bin:/usr/bin
# 设置换行模式以避免阶梯效应。
stty onlcr

echo "Running shutdown script $0:"
# 查找我们是如何被调用的。
case "$0" in
*0)
        message="The system is halted."
        command="halt"
        ;;
*6)
        message="Rebooting."
        command=reboot
        ;;
*)
        echo "$0: call me as \"rc.0\" or \"rc.6\" please!"
        exit 1
        ;;
esac
# 终止所有进程。
# INIT 现在应该完全处理这项工作，但在没有这种二次进程终止的情况下，这并不总是能正确工作。
# 因为 INIT 已经通知用户进程正在被终止，所以我们这次将避免回显此信息。
if [ "$1" != "fast" ]; then # shutdown 尚未终止所有进程
killall5 -15
killall5 -9
fi

# 尝试关闭配额和记账。
if [ -x /usr/sbin/quotaoff ]
then
    echo "Turning off quota."
    /usr/sbin/quotaoff -a
fi
if [ -x /sbin/accton ]
then
    echo "Turning off accounting."
    /sbin/accton
fi

# 在卸载文件系统之前，将重启或停机记录写入 wtmp。
$command -w

# 保存本地时间
[ -e /usr/lib/zoneinfo/localtime ] && cp /usr/lib/zoneinfo/localtime /etc

# 卸载所有远程文件系统：
echo "Unmounting remote file systems."
mount -a -tnfs

# 关闭交换分区，然后卸载本地文件系统。
echo "Turning off swap."
swapoff -a
echo "Unmounting local file systems."
mount -a -tnonfs
# 不要重新挂载 UMSDOS 根卷：
if [ ! "`mount | head -1 | cut -d ' ' -f 5`" = "umsdos" ]; then
    mount -n -o remount,ro /
fi

# 查看这是否是电力故障情况。
if [ -f /etc/power_is_failing ]; then
    echo "Turning off UPS, bye."
    /sbin/poword -q
    exit 1
fi

# 现在执行停机或重启。
echo "$Message"
[ ! -f /etc/fastboot ] && echo "On the next boot fsck will be FORCED."
$command -f
```

![](img/8ad518fddafc7f5e73715a2604b61d50_236_0.png)

Slackware Linux 系统最安全的运行级别是 0 —— 但在此级别下机器完全不可用。虽然任何程度的可用性都伴随着风险，但设置适当的运行级别至少可以提供一种实际的安全措施。例如，如果您将 Linux 用作路由器或防火墙，可以创建运行级别 2。系统中没有任何 X 运行。

# 系统初始化

在启动时，系统通过脚本 `/etc/rc.d/rc.S` 进行初始化。此脚本启动交换分区、挂载文件系统、配置系统时钟、加载模块，以及可能的 PCMCIA 和串行服务。如果您希望特定事件在系统启动时发生（例如，运行 PPP 连接），您可以将其添加到此脚本的末尾，如列表 7-5 所示。

### 列表 7-5：使用 /etc/rc.d/rc.S

```bash
#!/bin/sh
#
# /etc/rc.d/rc.S:  系统初始化脚本。
#
# 主要由:  Patrick J. Volkerding 编写. <volkerdi@ftp.cdrom.com>
#

PATH=/sbin:/usr/sbin:/bin:/usr/bin

# 启用交换
/sbin/swapon -a

# 启动更新。
/sbin/update &

# 自动模块加载。 要自动加载和卸载内核模块
# 根据需要，取消注释以下行以运行 kerneld。
# 在某些情况下，您需要创建别名以加载正确的
# 模块。 更多信息，请参见 /usr/doc/modules 中的文档。
# 注意：默认情况下这是被注释掉的，因为运行 kerneld
# 曾导致一些实验性内核在启动期间挂起。
#if [ -x /sbin/kerneld ]; then
#      /sbin/kerneld
#fi

# 测试根分区是否为只读；它应该是。
READWRITE=no
if echo -n > "/boot/Testing file system status"; then
rm -f "/boot/Testing file system status"
READWRITE=yes
fi

# 检查所有文件系统的完整性
if [ $READWRITE != yes ]; then
/sbin/fsck -A -a
# 如果有失败，进入单用户模式。
if [ $? -gt 1 ]; then
echo
echo
echo "*************************************"
echo "fsck returned error code - REBOOT NOW!"
echo "*************************************"
echo
echo
/bin/login
fi
# 以读写模式重新挂载根文件系统
echo "Remounting root device with read-write enabled."
/sbin/mount -w -n -o remount /
if [ $? -gt 0 ]; then
echo
echo "Attempt to remount root device as read-write failed! This is going to"
echo "cause serious problems...  "
echo
echo "If you're using the UMSDOS file system, you **MUST** mount the root"
echo "partition"
echo "read-write! You can make sure the root file system is getting mounted "
echo "read-write with the 'rw' flag to Loadlin:"
echo
echo "loadlin vmlinuz root=/dev/hda1 rw   (replace /dev/hda1 with your root"
echo "devices)"
echo
echo "Normal boot disks can be made to mount a system read-write with the rdev"
echo "command:"
echo
echo "rdev -R /dev/fd0 0"
echo
echo "You can also get into your system by using a bootkernel disk with a"
echo "command:"
echo "like this on the LILO prompt line:  (change the root partition name as"
echo "needed)"
echo
     echo "LiLO: mount root=/dev/hda1 rw"
     echo
     echo "Please press ENTER to continue, then reboot and use one of the above"
     echo -n "methods to"
     echo -n "get into your machine and start looking for the problem. "
     read junk;
fi
else
     echo "Testing filesystem status: read-write filesystem"
     if [ ! -d /DOS ]; then # no warn for UMSDOS (kind of a bad test, but...)
     cat << EOF
*** ERROR: Root partition has already been mounted read-write. Cannot check!

For file-system checking to work properly, your system must initially mount
the root partition as read-only. Please modify your kernel with 'rdev' so that
it does this. If you're booting with LiLO, add a line:

     read-only

to the Linux section in your /etc/lilo.conf and type 'lilo' to reinstall it.

If you boot from a kernel on a floppy disk, put it in the drive and type:
rdev -R /dev/fd0 1

If you boot from a bootkernel disk, or with Loadlin, you can add the 'ro' flag.

This will fix the problem *AND* eliminate this annoying message. :)
EOF
     echo -n "Press ENTER to continue. "
     read junk;
fi
fi

# 删除 /etc/mtab*，以便 mount 可以创建带有根条目的文件
/bin/rm -f /etc/mtab* /etc/nologin /etc/shutdownpid

# 挂载 fstab 中的文件系统（并为 / 创建条目）
# 但不包括 NFS，因为 TCP/IP 尚未配置
/sbin/mount -avt nonfs

# 清理 /var 卷上的临时文件：
/bin/rm -f /var/run/utmp /var/run/*.pid

# 看起来我们必须创建它。
cat /dev/null > /var/run/utmp

# 配置系统时钟。
# 如果您的系统保持 GMT，可以更改此项。
if [ -x /sbin/clock ]; then
        /sbin/clock -s
fi

# 设置 /etc/issue 和 /etc/motd 以反映当前内核级别：
# 这些会在每次启动时擦除您对 /ETC/ISSUE 和 /ETC/MOTD 所做的任何更改。
# 如果您想制作自定义版本，请将它们注释掉。
echo > /etc/issue
echo Welcome to Linux `bin/uname -a | bin/cut -d ' ' -f3` > /etc/issue
echo > /etc/issue
echo "`bin/uname -a | bin/cut -d ' ' -f1,3`" > /etc/motd

# 这会加载任何所需的内核模块。这些可能是使用
# 您的 CD-ROM 驱动器、总线鼠标、以太网卡或其他可选硬件所必需的。
if [ -x /etc/rc.d/rc.modules ]; then
        . /etc/rc.d/rc.modules
fi

# 初始化 PCMCIA 设备：
#
# 注意：这曾更接近此脚本的顶部，以便 PCMCIA 设备
# 可以与其他驱动器一起进行 fsck。然而，这有一些不幸的
# 副作用，因为 root 尚未变为读写，且 /var 甚至可能
# 未挂载，pid 文件无法正确写入 /var/run，
# 且 pcmcia 系统无法正确关闭。如果您希望某些 PCMCIA
# 分区在启动时（或插入卡时）被挂载，则请添加
# 适当的行到 /etc/pcmcia/scsi.opts。
#
if [ -x /etc/rc.d/rc.pcmcia ]; then
        . /etc/rc.d/rc.pcmcia start
fi

# 运行串口设置脚本：
# （小心！如果 rc.serial 脚本未正确设置，这可能导致某些系统挂起。
# 如果发生这种情况，您可能需要使用启动盘编辑该文件）
#
# . /etc/rc.d/rc.serial
```

