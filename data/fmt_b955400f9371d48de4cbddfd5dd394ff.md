
![](img/3f35ec29a294974bc1a4fdae3ae46652_346_0.png)

在主菜单上除了 `Enter` 键外，还有三个可用命令，`Enter` 键会启动选中的操作系统。命令在表 15-2 中列出并解释。

| 命令 | 描述 |
| --- | --- |
| a | 添加或修改内核参数。 |
| c | 进入 `grub>` 命令行提示符。 |
| e | 在启动前编辑选定条目的的指令。 |

表 15-2 GRUB 主菜单命令

图 15-2 显示了在 GRUB 菜单中输入 `e` 时显示的启动指令。

![](img/3f35ec29a294974bc1a4fdae3ae46652_347_0.png)

图 15-2 GRUB 菜单启动信息

GRUB 的编辑菜单中有几个可用命令，这些命令在表 15-3 中列出并描述。

| 命令 | 描述 |
| --- | --- |
| b | 启动操作系统。 |
| c | 进入 `grub>` 命令行提示符。 |
| e | 编辑选定的指令。 |
| d | 删除选定的行条目。 |
| o | 在选定的行条目之后打开新行。 |
| O | 在选定的行条目之前打开新行。 |
| Esc | 返回主菜单。 |

表 15-3 GRUB 编辑菜单命令

# 启动示例

如所述，系统可以从 GRUB 菜单启动到不同的 rc 级别（level）。以下文本解释了如何操作。

## 启动到单用户模式

将系统启动到单用户模式允许你执行维护任务，例如更改忘记的 root 密码、修改损坏的 `passwd`、`shadow` 或 `fstab` 文件，或执行 `fsck`。按照以下说明启动到此模式：

308 红帽认证技术人员与工程师

1. 在倒计时结束前按任意键与 GRUB 交互。
2. 按 `a` 进入追加模式。
3. 按空格键并输入 `l, s`，或者输入 `single` 然后按回车键进行启动。
4. 执行任何所需的维护任务。
5. 完成后，执行 `exit` 命令启动到默认运行级别。或者，发布 `reboot` 或 `shutdown` 命令将系统重启到默认运行级别。

## 启动到 rc 级别 2 或 3

将系统启动到 rc 级别 2 或 3 会启动大多数系统服务。按照以下说明：

1. 在倒计时结束前按任意键与 GRUB 交互。
2. 按 `a` 进入追加模式。
3. 按空格键并输入所需的 rc 级别。按回车键启动。

## 启动到紧急模式

将系统启动到紧急模式允许你在无法启动的系统上执行某些维护任务。按照以下说明：

1. 在倒计时结束前按任意键与 GRUB 交互。
2. 按 `a` 进入追加模式。
3. 按空格键并输入 `emergency`。按回车键启动。在进入紧急模式时输入 `root` 用户密码。
4. 执行任何所需的维护任务。
5. 完成后，执行 `exit` 命令启动到默认运行级别。或者，发布 `reboot` 或 `shutdown` 命令将系统重启到默认运行级别。

## 启动到救援模式

详情请参见“系统、网络与安全故障排除”章节中的“将系统启动到 Linux 救援模式”部分。

# 理解 GRUB 配置文件

了解位于 `/boot/grub/` 目录下的 GRUB 配置文件 `grub.conf` 的内容非常重要。该文件拥有 `/etc/grub.conf` 和 `/boot/grub/menu.lst` 文件的符号链接。以下是默认文件的摘：

```
# nl /boot/grub/grub.conf
...
10 default=0
11 timeout=5
12 splashimage=(hd0,0)/grub/splash.gz
13 hiddenmenu
14 title Red Enterprise Linux Server (2.6.18-92.el5)
15 root (hd0,0)
16 kernel=/vmlinuz-2.6.18-92.el5 root=/dev/VolGroup0/lv1 quiet
17 initrd/initrd-2.6.18-92.img
```

文件的内容解释如下：

- 第 10 行：设置与相应的“title”定义的默认内核，如果值设置为 1，它将指向下一个与“title”相关的内核。
- 第 11 行：给你 5 秒时间中断自动启动以与 GRUB 菜单交互。
- 第 12 行：设置图形 GRUB 屏幕。位于 `/boot/grub/splash.gz` 的第一个分区。
- 第 13 行：指示系统在按下键前隐藏 GRUB 菜单。
- 第 14 行：指定可用内核的名称或简短描述。
- 第 15 行：指向启动分区的位置。在 `/boot/grub/device.map` 中定义的第一个分区。

```
#boot/grub/device.map
(hd0)/dev/sda
```

- 第 16 行：指定内核名称及其位于 `/boot` 的位置。表示从 `dev/VolGroup0/root` 以图形模式（Red Hat Boot）启动带有“quiet”。
- 第 17 行：初始化 RAM 磁盘并从 `/boot/initrd-2.6.18-92.img` 启动初始根。当内核构建时，可以使用 `mkinitrd` 重新创建此文件。

# 管理 GRUB

在 `grub>` 提示符处有许多命令用于 GRUB 和其他任务。在 `grub>` 提示符处按 `TAB` 键查看列表。本节演示了其中命令的用法![](img/3f35ec29a294974bc1a4fdae3ae46652_349_0.png)

查找 `/boot/grub` 目录下包含 `grub.conf` 的磁盘和分区：

```
grub> find /boot/grub.conf
(hd0,0)
```

查看 `grub.conf` 的内容：

```
grub> cat /boot/grub.conf
```

获取根分区的信息：

```
grub> root
(hd0,0): Filesystem is ext2fs, partition type 0x7
```

加载硬盘第一个分区上的根分区：

```
grub> root (hd0,0)
Filesystem is ext2fs, partition type 0x7
```

如果 MBR 已损坏则安装 GRUB：

```
grub> setup (hd0)
Checking if /boot/grub/stage1... no
Checking if /boot/stage1... yes
Checking if /boot/stage2... yes
Checking if /boot/e2fs_stage1... yes
Running "embedded/e2fs_stage1"... succeeded
Running "install/grub/e2fs_stage1 (hd0) (hd0,0)/stage2 /grub.conf...Done.
```

# 启动 - 内核初始化阶段

GRUB 初始化内核并加载到内存中。在初始化期间，控制台上会出现取决于硬件和系统配置这些消息记录在 `/var/log/dmesg` 中，稍可以使用 `dmesg` 命令查看。消息包含了有关内核、内存、控制台、SELinux 状态、磁盘、根卷或分区、网络接口以及交换卷/分区的信息。

`/var/log/dmesg` 摘：

```
# cat /var/log/dmesg
Linux version 2.6.18-92.el5 (brewbuilder@hs20-bc2-3.redhat.com) (gcc version 4.1.2 20070124) #1 SMP Tue Apr 29 13:16:12 EDT 2008
BIOS-提供的物理 RAM 映射:
BIOS-e280: 0000000000000000-000000000000099f800 (usable)
BIOS-e280: 0000000000000000-000000000000a000 (reserved)
---------------------------------------
0MB HIGHMEM 可。
416MB LOWMEM 可。
在 000f6ce0 找到 SMP MP-表
内核内存 (0x0 到 0xf0) 在允许范围内
禁用 imap
使用 x86 段限制来近似 NX 保护
节点 0 的总页数: 106496
---------------------------------------
DMA 区域: 4096 页, LIFO 批量:0
Normal 区域: 102400 页, LIFO 批量:31
DMI present.
```

# 关

311

GRUB 初始化内核将其加载到内存中。在初始化期间，控制台上会出现若干取决于硬件和系统配置的消息。这些消息记录在 `/var/log/dmesg` 中，稍可以使用 `dmesg` 命令查看。消息包含了有关内核、内存、控制台、SELinux 状态、磁盘、根卷或分区、网络接口以及交换卷/分区的信息。

## 理解 /etc/inittab 文件
