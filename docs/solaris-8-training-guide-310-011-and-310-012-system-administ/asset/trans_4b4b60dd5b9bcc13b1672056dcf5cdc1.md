
这些信息包括要使用的数据库、支持的标签、要使用的设备、特定媒体事件发生时要采取的操作，以及在不卸载的情况下不安全弹出的文件系统列表。vold.conf 文件如下所示：

```
# @(#)vold.conf 1.25      99/11/11 SMI
#
# Volume Daemon Configuration file
#
# Database to use (must be first)
db db_mem.so
# Labels supported
label cdrom label_cdrom.so cdrom
label dos label_dos.so floppy rmdisk pcmem
label sun label_sun.so floppy rmdisk pcmem
# Devices to use
use cdrom drive /dev/rdsk/c*s2 dev_cdrom.so cdrom%d
use floppy drive /dev/rdiskette[0-9] dev_floppy.so floppy%d
use pcmem drive /dev/rdsk/c*s2 dev_pcmem.so pcmem%d forceload=true
use rmdisk drive /dev/rdsk/c*s2 dev_rmdisk.so rmdisk%d
# Actions
eject dev/diskette[0-9]/* user=root /usr/sbin/rmmount
eject dev/dsk/* user=root /usr/sbin/rmmount
insert dev/diskette[0-9]/* user=root /usr/sbin/rmmount
insert dev/dsk/* user=root /usr/sbin/rmmount
notify rdsk/* group=tty user=root /usr/lib/vold/volmissing -p
remount dev/diskette[0-9]/* user=root /usr/sbin/rmmount
remount dev/dsk/* user=root /usr/sbin/rmmount
# List of file system types unsafe to eject
unsafe ufs hsfs pcfs udfs
```

vold.conf 文件中的每个部分都用其功能进行了标记。在这些部分中，您可以安全地修改“要使用的设备”，其描述见表 7.9，以及“操作”，其描述见表 7.10。

“要使用的设备”部分描述了 vold 要管理的设备。vold 的语法如下：

```
use <device> <type> <special> <shared_object> <symname> [ options ]
```

## 表 7.9
### VOLD.CONF 要使用的设备

| 参数字段 | 描述 |
|---|---|
| device | 要使用的可移动媒体设备类型。合法值是 cdrom 和 floppy。 |
| type | 设备的特定功能。合法值是 drive。 |
| special | 指定要使用的设备或设备。路径通常以 /dev 开头。 |
| shared_object | 管理此设备的程序的名称。vold 预计在 /usr/lib/vold 中找到此程序。 |
| symname | 引用此设备的符号名称。symname 放在设备目录中。 |
| options | 插入介质的用户、组和模式权限（可选）。 |

special 和 symname 参数相关。如果 special 包含任何 shell 通配符（即其中有一个或多个星号或问号），则 symname 必须以 %d 结尾。在这种情况下，找到匹配正则表达式的设备会被排序然后编号。第一个设备用 0 填充 %d，第二个找到的设备用 1，以此类推。

如果 special 规范不包含 shell 通配符，则 symname 参数必须在其末尾明确指定一个数字。

“操作”部分指定如果发生特定事件（操作）应调用哪个程序。Actions 字段的语法如下：

```
insert regex [ options ] <program> <program_args>
eject regex [ options ] <program> <program_args>
notify regex [ options ] <program> <program_args>
```

不同操作列在表 7.10 中。

## 表 7.10
### VOLD.CONF 操作

| 参数 | 描述 |
|---|---|
| insert|eject|notify | 触发事件的媒体操作。 |
| regex | 此 Bourne shell 正则表达式与受此事件影响的 /vol 文件系统中的每个条目进行匹配。 |
| [options] | 指定此事件要运行的用户或组名（可选）。 |
| <program> | 如果 regex 匹配，则要运行的可执行程序的完整路径名。 |
| program_args | 程序的参数。 |

在默认的 vold.conf 文件中，您会在“要使用的设备”和“操作”部分下看到以下条目：

```
# Devices to use
use cdrom drive /dev/rdsk/c*s2 dev_cdrom.so cdrom%d
use floppy drive /dev/rdiskette[0-9] dev_floppy.so floppy%d
use pcmem drive /dev/rdsk/c*s2 dev_pcmem.so pcmem%d forceload=true
use rmdisk drive /dev/rdsk/c*s2 dev_rmdisk.so rmdisk%d
# Actions
eject dev/diskette[0-9]/* user=root /usr/sbin/rmmount
eject dev/dsk/* user=root /usr/sbin/rmmount
insert dev/diskette[0-9]/* user=root /usr/sbin/rmmount
insert dev/dsk/* user=root /usr/sbin/rmmount
notify rdsk/* group=tty user=root /usr/lib/vold/volmissing -p
remount dev/diskette[0-9]/* user=root /usr/sbin/rmmount
remount dev/dsk/* user=root /usr/sbin/rmmount
```

当 CD 插入到名为 /dev/dsk/c0t6d0 的 CD-ROM 时，会发生以下情况：

- 1. vold 检测到 CD 已插入，并运行 /usr/sbin/rmmount 命令。rmmount 是自动在 CD-ROM 和软盘上挂载文件系统的实用程序。它确定介质上是否存在的文件系统类型（如果有）。如果存在文件系统，rmmount 会挂载文件系统（对于 CD-ROM，在 /cdrom0 中）。

如果介质是只读的（CD-ROM 或写保护标签已设置的软盘），则文件系统以只读方式挂载。如果未识别出文件系统，rmmount 不会挂载文件系统。

- 2. 挂载完成后，将执行与媒体类型关联的操作。该操作允许其他程序被通知有新的介质可用。例如，挂载 CD-ROM 或软盘的默认操作是启动文件管理器。

这些操作在配置文件 `/etc/rmmount.conf` 中有描述。以下是默认 `/etc/rmmount.conf` 文件的示例：

```
# @(#)rmmount.conf 1.10      00/02/14 SMI
#
# Removable Media Mounter configuration file.
#
# File system identification
ident udfs ident_udfs.so cdrom floppy rmdisk
ident hsfs ident_hsfs.so cdrom
ident ufs ident_ufs.so cdrom floppy rmdisk pcmem
ident pcfs ident_pcfs.so floppy rmdisk pcmem
# Actions
action cdrom action_filemgr.so
action floppy action_filemgr.so
action rmdisk action_filemgr.so
# Mount
mount * hsfs udfs ufs -o nosuid
```

- 3. 如果用户发出 eject 命令，vold 会看到媒体事件，并执行与该事件关联的操作。在这种情况下，它运行 `/usr/sbin/rmmount`。rmmount 卸载已挂载的文件系统，并执行 `/etc/rmmount.conf` 文件中指出的与媒体类型关联的操作。如果文件系统“忙”（即它包含活动进程的当前工作目录），则 eject 操作失败。

系统管理员可以修改 vold.conf 以指定在发生媒体事件（如 eject 或 insert）时应调用哪个程序。如果修改了 vold.conf 配置文件，必须通知 vold 重新读取 `/etc/vold.conf` 文件。按如下方式停止并启动 vold 即可完成此操作。输入以下内容：

/etc/init.d/volmgt stop

然后输入以下内容：

/etc/init.d/volmgt start

还有一些其他命令可以帮助您在系统上管理卷管理器。它们在表 7.11 中有描述。

## 表 7.11
### 卷管理器命令

| 命令 | 描述 |
|---|---|
| rmmount | 可移动媒体挂载器。vold 在安装 CD 或软盘时用于自动挂载 /cdrom 和 /floppy。 |
| volcancel | 取消用户访问特定 CD-ROM 或软盘文件系统的请求。此命令由系统管理员发出，如果包含文件系统的可移动介质当前不在驱动器中，则很有用。 |
| volcheck | 系统管理员发出此命令以检查驱动器中是否安装了介质。默认情况下，它检查由 /dev/diskette 指向的驱动器。 |
| volmissing | 此操作在 vold.conf 中指定，如果尝试访问已不在驱动器中的 CD 或软盘，则会通知用户。 |
| vold | 卷管理器守护进程，由 /etc/vold.conf 控制。 |

对某些人来说，卷管理可能弊大于利。要禁用卷管理，请删除（或重命名）名为 /etc/rc2.d/S92volmgt 的文件。然后发出命令 /etc/init.d/volmgt stop。如果您希望 CD 上有卷管理但软盘上没有，请在 vold.conf 文件的“要使用的设备”和“操作”部分中用 # 注释掉条目，如下所示：

```
# Devices to use
use cdrom drive /dev/rdsk/c*s2 dev_cdrom.so cdrom%d
#use floppy drive /dev/rdiskette[0-9] dev_floppy.so floppy%d
use pcmmem drive /dev/rdsk/c*s2 dev_pcmmem.so pcmmem%d forceload=true
# use rmscsi drive /dev/rdsk/c*s2 dev_rmscsi.so rmscsi%d

# Actions
#insert dev/diskette[0-9]/* user=root /usr/sbin/rmmount
insert dev/dsk/* user=root /usr/sbin/rmmount
#eject dev/diskette[0-9]/* user=root /usr/sbin/rmmount
eject dev/dsk/* user=root /usr/sbin/rmmount
notify rdsk/* group=tty user=root /usr/lib/vold/volmissing -p
```
