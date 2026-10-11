
现在你已经看到了 RHEL5 上的启动过程，让我们重新开始介绍 RHEL6 中新的 Upstart 进程。Upstart 是基于事件的，因此它不需要按顺序处理所有内容（与 RHEL5 不同）。每个进程对 Upstart 都是已知的，任务在 `/etc/init` 目录中定义。`init` 进程仍然是首先创建的；然而，它来自一个 Upstart 事件。不是调用 `rc.sysinit` 主脚本（该脚本反过来调用每个运行级别），而是 Upstart 从目录中启动一个作业来继续启动过程。`/etc/initab` 文件已被弃用，仅为 `initdefault` 定义的默认运行级别进行查询。

# 50 Hands-on Guide to the Red Hat® Exams: RHCSA™ and RHCE® Cert Guide and Lab Manual

```bash
# 捕捉 CTRL-ALT-DELETE
ca::ctrlaltdel:/sbin/shutdown -t3 -r now

# 当我们的 UPS 告诉我们断电时，假设我们还有一些
# 电量。安排在 2 分钟后关机。
# 当然，这假设你安装了电源并且你的
# UPS 连接并正常工作。
pf::powerfail:/sbin/shutdown -f -h -2 "Power Failure; System Shutting Down

# 如果在关机触发之前恢复恢复，则取消。
pr:12345:powerwait:/sbin/shutdown -c "Power Restored; Shutdown Cancelled
```

```bash
# 在标准运行级别下运行 getty
1:2345:respawn:/sbin/mintty tty1
2:2345:respawn:/sbin/mintty tty2
3:2345:respawn:/sbin/mintty tty3
4:2345:respawn:/sbin/mintty tty4
5:2345:respawn:/sbin/mintty tty5
6:2345:respawn:/sbin/mintty tty6
```

```bash
# 在运行级别 5 下运行 xdm
x:5:respawn:/etc/x11/prefd -nodemon
```

从这个文件中，你可以看到默认运行级别被设置为 5，尽管列出了不同的运行级别。`/etc/initab` 文件定义了如何处理断电和虚拟终端。在 `init` 进程完成 `/etc/initab` 文件后，会运行 `/etc/rc.d/rcinit` 脚本，它处理系统时钟、网络、设置用户环境等。

在 Red Hat Enterprise Linux 中，默认运行级别是 5，正如检查 `/etc/initab` 文件所示。这个默认运行级别被传递给 `/etc/rc.d` 脚本，该脚本调用 `/etc/rc.d/rc#` 中的所有程序。你最后看到的应该是登录提示符。如果你安装了 Gnome 等桌面管理器，你将看到一个 GUI 屏幕，可以在其中登录系统；否则，使用文本模式登录。这完成了启动过程。

## RHEL6 grub 配置变更

配置文件，但这是 RHEL6 发生变化的一个区域。首先，让我们来看旧版的 `grub.conf` 版本：

```bash
# cat /boot/grub/grub.conf
default=0
timeout=5
splashimage=(hd0,0)/grub/splash.xpm.gz
hiddenmenu
title Red Hat Enterprise Linux Server (2.6.18-we92.e15)
  root (hd0,0)
  kernel /vmlinuz-2.6.18-we92.e15 root=/dev/VolGroup00/LogVol00 rhgb quiet
  initrd /initrd-2.6.18-we92.e15.img
```

在前面的示例中，你可以看到有一个启动选项，由 `title` 条目定义。这也被称为条目 0，因此它成为了默认的启动内核。你还可以看到正在使用的内核版本，以及根分区在启动过程中挂载的位置。如果你想添加额外的启动选项，可以添加其他带有选项的内容作为第二个启动选择。这个 `grub.conf` 包含了确保启动过程正常的所有内容。现在让我们来看 RHEL6 的新版本 `grub.conf` 文件：

```bash
# cat grub.conf
default=0
timeout=5
splashimage=(hd0,0)/grub/splash.xpm.gz
hiddenmenu
title Red Hat Enterprise Linux (2.6.32-71.e16)
  root (hd0,0)
  kernel /vmlinuz-2.6.32-71.e16 root=/dev/mapper/vg01-lv_root rhgb quiet
  initrd /initramfs-2.6.32-71.e16.img
```
