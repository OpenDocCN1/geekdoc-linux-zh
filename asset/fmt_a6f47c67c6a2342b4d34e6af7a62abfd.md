
```
1 [rich@shadrach@dev]$ ls -al sda* tty$
2 br-rw-- 1 root disk          8, 0 May 1998 sda
3 br-rw-- 1 root disk          8, 1 May 1998 sda1
4 br-rw-- 1 root disk          8, 10 May 1998 sda10
5 br-rw-- 1 root disk          8, 11 May 1998 sda11
6 br-rw-- 1 root disk          8, 12 May 1998 sda12
7 br-rw-- 1 root disk          8, 13 May 1998 sda13
8 br-rw-- 1 root disk          8, 14 May 1998 sda14
9 br-rw-- 1 root disk          8, 15 May 1998 sda15
10 br-rw-- 1 root disk          8, 2 May 1998 sda2
11 br-rw-- 1 root disk          8, 3 May 1998 sda3
12 br-rw-- 1 root disk          8, 4 May 1998 sda4
13 br-rw-- 1 root disk          8, 5 May 1998 sda5
14 br-rw-- 1 root disk          8, 6 May 1998 sda6
15 br-rw-- 1 root disk          8, 7 May 1998 sda7
16 br-rw-- 1 root disk          8, 8 May 1998 sda8
17 br-rw-- 1 root disk          8, 9 May 1998 sda9
18 br-rw-- 1 root tty          6, 64 Nov 29 16:09 ttyS0
19 cr-rw-- 1 root tty          4, 65 May 1998 ttyS1
20 cr-rw-- 1 root tty          4, 66 May 1998 ttyS2
21 cr-rw-- 1 root tty          4, 67 May 1998 ttyS3
22 [rich@shadrach@dev]$
```

第 1 行显示了用于 `ls` 命令来显示 `sda` 和 `tty` 设备的所有条目。`sda` 设备是第一个 SCSI 驱动器，而 `tty` 设备是标准的 IBM PC 串口端口。第 2 到 17 行显示了 Linux 系统上创建的所有 `sda` 设备。并不是所有的设备都被实际使用，但它们是在管理员需要时创建的。第 18 到 21 行显示了所有创建的 `tty` 设备。

第五列显示了主设备节点号。注意所有 `sda` 设备具有相同的主设备节点号。`sda` 设备的主设备节点号为 8，`tty` 设备使用 4。第六列显示了次设备号。每个内核都有自己的次设备号。

# Linux 简介

## 第 2 章

内核模块指示了权限。第一列指示了文件类型。注意所有磁盘文件都被标记为 `(b)`，而串口设备文件被标记为 `(c)`。

要创建一个新的设备节点，使用 `mknod` 命令。`mknod` 的格式为：

```
mknod [OPTION] NAME TYPE
```

其中 `NAME` 是文件名，`TYPE` 是。

## 文件系统管理

如之前所述，在旧版本的 Linux 内核中，为设备添加新驱动并不是一项容易的任务。必须重新编译整个内核以插入新驱动。的是，这个问题已经解决了。现在 Linux 内核支持模块，即可以在内核运行时插入和移除的驱动。这是 Linux 内核开发的一个重大突破。

可以使用 `insmod` 命令将模块插入到运行的内核中。`insmod` 命令的格式为：

```
insmod [ -fkmpsXX ] [ - module_name ] object_file [ symbol=value
```

`insmod` 程序尝试将指定的 `object_file` 代码链接到运行的内核。表 2.5 显示了与 `insmod` 使用的命令行选项。Linux 可以读取和写入的文件系统有 15 种。

| 文件系统 | 说明 |
|---|---|
| affs | Amiga 文件系统 |
| ext | 扩展文件系统 |
| ext2 | 第二扩展文件系统 |
| hpfs | OS/2 高性能文件系统 |
| iso9660 | ISO 9660 文件系统（光盘） |
| minix | MINIX 文件系统 |
| msdos | Microsoft FAT16 |
| ncp | NetWare 文件系统 |
| nfs | 网络文件系统 |
| proc | 系统信息 |
| smb | Samba 文件系统 |
| sysv | 旧 Unix 文件系统 |
| ufs | Solaris 和 SunOS 文件系统 |
| umsdos | 位于 MS-DOS 之上的类 Unix 文件系统 |
| vfat | Windows 95 文件系统 |
| xia | 类似于 ext2 |

# Linux 简介

## 第 2 章

`insmod` 程序将模块代码链接到内核代码中，但这只是暂时的添加。当 Linux 服务器重启时，旧内核将加载且不包含这些添加的模块。解决此问题的方案是 `modprobe` 程序。

`modprobe` 程序可以根据一组配置文件将一组模块加载到内核中。`modprobe` 命令的格式如下：

```
modprobe module.o [symbol=value ...]
modprobe -t tag pattern
modprobe -a -t tag pattern
modprobe -l [ t tag ]
modprobe -r module
modprobe -c
```

`modprobe` 命令的第一种格式用于将单个模块加载到内核中。如果模块需要任何参数，可以在命令行输入这些参数。`-t` 选项允许 `modprobe` 加载模式列表中所有匹配特定标签的模块。`-r` 选项用于从内核中移除特定的模块。

模块列表可以放置在启动时可访问的文件中。在 Mandrake Linux 6.0 版本中，模块的位置位于 `/lib/modules/2.2.9-19mdk/modules.dep`。

该文件包含了 `modprobe` 命令在启动时尝试安装到内核的所有所有模块列表。可以使用 `depmod` 程序从模块列表中添加或删除模块。

另一个用于 `modprobe` 的配置文件是 `/etc/conf.modules` 文件。此配置行决定了 `modprobe` 程序的行为。表 2.6 显示了可以在此使用的配置行。

### 表 2.6 /etc/conf.modules 文件命令

| 命令 | 描述 |
|---|---|
| keep | 指导 `modprobe` 将任何定义的项添加到 conf 文件中，而不是替换 |
| path=MOD_PATH | 指定搜索模块的目录 |
| path[tag]=MOD_PATH | 为位于目录的模块指定标签 |
| alias module real-name | 指定一个别名来引用模块名 |
| pre-install module command | 在安装模块之前执行命令 |
| install module command | 在模块安装时执行命令 |
| post-install module command | 在模块安装后执行命令 |
| pre-remove module command | 在移除模块正之前执行命令 |
| remove module command | 在移除模块时执行命令 |
| post-remove module command | 在移除模块后执行命令 |

列表 2.6 显示了一个 `/etc/conf.modules` 文件的示例。

### 列表 2.6 示例 /etc/conf.modules 文件

```
1 alias scsi_hotadadapter aic7xxx
2 alias eth0 3c59f
3 alias parport_lowlevel portant_pc
4 pre-install pcmia_core /etc/rc.d/init.d/pcmcia start
```

第 1 到 3 行为模块列表中加载的通用设备定义了别名。每个通用设备指向将加载的模块文件的真实名称。第 4 行显示了在加载 `pcmcia` 模块之前应该运行的程序。

## 内核版本

Linux 内核的发展非常迅速。Linus Torvalds 对 Linux 内核保持严格控制，尽管他接受来自任何人、任何地方的请求。多年来，Linux 内核设计取得了许多进展，例如模块的引入。

内核开发者使用严格的版本控制系统。内核发布版本的格式为：

```
linux-a.b.c
```
