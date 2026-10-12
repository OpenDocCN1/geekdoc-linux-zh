
该配置文件显示了三个示例段（`stanzas`）。第一个从第一个磁盘上的第一个分区（`hda1`）启动 `Red Hat`。第二个启动段从下一个分区启动 `Suse 8.0`。最后一个加载 `MS-DOS`。

## 14.5. 练习：启动器

* 找出你的系统使用的是 `lilo`、`grub` 还是 `grub2`。仅进行适用于你系统的练习。
* 复制 `/boot` 中的内核（`kernel`）、`initrd` 和 `System.map` 文件。将这些副本也放在 `/boot` 中，但将 `2.x` 或 `3.x` 替换为 `4.0`（假设 `Linux 4.0` 已经发布）。
* 在 `grub` 中为 `4.0` 文件添加一个段。确保标题与众不同。
* 将启动菜单超时设置为 `30` 秒。
* 重启并测试新的段。

## 14.6. 答案：启动器

0. 找出你的系统使用的是 `lilo`、`grub` 还是 `grub2`。仅进行适用于你系统的练习。

1. 复制 `/boot` 中的内核、`initrd` 和 `System.map` 文件。将副本也放在 `/boot` 中，但将 `2.x` 或 `3.x` 替换为 `4.0`（假设 `Linux 4.0` 已经发布）。

```bash
[root@centos65 #]# uname -r
2.6.0.32-431.11.2.el16.x86_64
[root@centos65 #]# cp System.map-2.6.0.32-431.11.2.el16.x86_64 System-map-4.0
[root@centos65 #]# cp vmlinuz-2.6.0.32-431.11.2.el16.x86_64 vmlinuz-4.0
[root@centos65 #]# cp initramfs-2.6.0.32-431.11.2.el16.x86_64.img initramfs-4.0.img
```

不要忘记 `initrd` (`initramfs`) 文件以 `.img` 结尾。

2. 在 `menu.lst` 为 `grub2` 添加一个段。确保该段格式正确。

```bash
[root@centos65 grub]# cut -c70 menu.lst | tail -12
title CentOS (4.0)
root (hd0)
kernel vmlinuz-4.0 ro=/dev/mapper/VolGroup-lv_root rd_NO_LUKS L
initrd/initramfs-4.0.img
title CentOS (2.6.32-431.11.2.el16.x86_64)
kernel vmlinuz-2.6.32-431.11.2.el16.x86_64 ro=/dev/mapper/VolGroup0
initrd/initramfs-2.6.32-431.11.2.el16.x86_64.img
title CentOS (2.6.32-431.11.2.el16.x86_64)
kernel vmlinuz-2.6.32-431.11.2.el16.x86_64 ro=/dev/mapper/VolGroup-lv
initrd/initramfs-2.6.32-431.11.2.el16.x86_64.img
```

3. 将启动超时设置为 `30` 秒。

```bash
[root@centos65 grub]# vi menu.lst
[root@centos65 grub]# grep timeout /boot/grub/grub.conf
timeout=30
```

4. 重启并测试新的段。

```bash
[root@centos65 #]# reboot
```

![](img/b73e4add6be31135074237b0a665e1f4_176_0.png)

选择你的段，如果它能启动，说明你是正确的。

# 第 15 章. `init` 和运行级别

许多 `Unix` 和 `Linux` 发行版使用 `init` 脚本来启动守护进程，正如 `Unix System V` 那样。本章将详细解释其工作原理。

`Init` 使用脚本启动守护进程，每个脚本启动一个守护进程，并且每个脚本等待上一个脚本。这种串行启动守护进程的过程缓慢，虽然对于运行时间以年计算的服务器来说启动慢不是问题，但最近 `Linux` 在桌面端的普及导致了抱怨。为了提高 `Linux` 的启动速度，`Canonical` 开发了 `upstart`，首次用于 `Ubuntu`。`Solaris` 也使用了 `Service Management Facility`。这两个系统都并行启动守护进程，并可以取代 `SysV init`（下一代）。2014 年，`systemd` 倡议领先，`Fedora`、`RHEL7` 和 `CentOS7` 也选择了它作为 `init` 的首选替代方案。

## 系统 初始化

## 15.1.1 内核进程 `ID 1`

内核从启动器接收控制权。一段时间后，内核启动 `init` 守护进程 (`/sbin/init`)，它是第一个启动的守护进程并接收进程 `ID 1` (`PID 1`)。它永远不会死亡。

## 15.1.2. `/etc/init` 中的配置

当 `/sbin/init` 启动时，它会首先读取其配置文件 `/etc/init`。在该文件中，它会寻找 `initdefault` 的值（见下方截图）。

```bash
[paul@rhel4 ~]$ grep ^id /etc/init
id=3:default
```

## 15.1.3. `initdefault`

`initdefault` 中的值表示默认运行级别。某些 `Linux` 发行版在 `/etc/init` 中对运行级别有简短描述。

`Init` 使用脚本启动守护进程，其中每个脚本启动一个守护进程，并且每个脚本等待上一个脚本。这种串行启动守护进程的过程缓慢，虽然对于运行时间以年计算的服务器来说启动慢不是问题，但最近 `Linux` 在桌面端的普及导致了抱怨。为了提高 `Linux` 的启动速度，`Canonical` 开发了 `upstart`，首次用于 `Ubuntu`。`Solaris` 也使用了 `Service Management Facility`。这两个系统都并行启动守护进程，并可以取代 `SysV init`（下一代）。2014 年，`systemd` 倡议领先，`Fedora`、`RHEL7` 和 `CentOS7` 也选择了它作为 `init` 的首选替代方案。

## 系统 初始化

## 15.1.1 内核进程 `ID 1`

内核从启动器接收控制权。一段时间后，内核启动 `init` 守护进程 (`/sbin/init`)，它是第一个启动的守护进程并接收进程 `ID 1` (`PID 1`)。它永远不会死亡。

## 15.1.2 `/etc/init` 中的配置

当 `/sbin/init` 启动时，它会首先读取其配置文件 `/etc/init`。在该文件中，它会寻找 `initdefault` 的值（见下方截图）。

```bash
[paul@rhel4 ~]$ grep ^id /etc/init
id=3:default
```
