
# `$()vold.conf 1.25 99/11/11 SMI`

## 卷守护进程配置文件

### 使用的数据库（必须在第一行）
`d db_mem.so`

### 支持的标签
`label cdrom label_cdrom rmdisk pcmcm`
`label usb_disk.flo floppy rmdisk pcmcm`
`label sur_label_sun.so floppy rmdisk pcmcm`

### 使用的设备
`cuse drive /dev/rdsk/c22 dev_cdrom.so cdrom@`
`cuse floppy drive /dev/rdiskette[0-9] dev_floppy floppykd`
`cuse drive /dev/rdsk/c22 dev_pcmkm.so pcmkm@ forcelastructure`
`cuse rmdisk /dev/rdsk/c22 dev_rmdisk.so rmdisk@`

### 操作
`deject dev/diskette[0-9] /user-root /usr/sbin/rmount`
`deject dev/dak/* /user-root /usr/sbin/rmount`
`insert dev/diskette[0-9] /user-root /usr/sbin/rmount`
`insert dev/dak/* /user-root /usr/sbin/rmount`
`ground dev/diskette[0-9] /usr/lib/vold/volmissing -p`
`remount dev/diskette[0-9] /user-root /usr/sbin/rmount`
`remount dev/dak/* /user-root /usr/sbin/rmount`

### 不安全退出的文件类型列表

![](img/fc66b89f230af58e50f0f6d09ca0496d_708_0.png)

## 卷管理
`unsafe ufs hfs5 pcfs udfs`

`/etc/vold.conf` 文件的语法所示。

```
# 使用的数据库
db database

# 支持的标签
label_type shared_object device

# 使用的设备
use device special shared_object syname [ options ]

# 操作
insert-regex [ options ] program program args
eject regex [ options ] program program args
notify regex [ options ] program program args

# 不安全退出的文件类型列表
unsafe fs_type fs_type
```

你可以安全地仅修改“使用的设备”（Devices to use）和“操作”（Actions）字段。你不应对对任何其他字段进行任何更改。

如果你修改了 `vold.conf` 文件，必须向其发送一个 HUP 信号以告诉它重新读取 `vold.conf`，如下所示。

```
# ps -ef -- grep vold
root 252 1 10:38:29 ? 0:02 /usr/sbin/vold
winsor 500 42
```

# 662

## 卷管理
收集调试信息的另一种方法是运行带有调试选项的 `rmmount` 命令。要为此，请编辑 `/etc/vold.conf`，并将包含 `/usr/sbin/rmmount` 的行修改为包含 `-D` 选项，例所示。

```
insert /vol*/dev/diskette[0-9]* user@root /usr/sbin/rmmount -D
```
