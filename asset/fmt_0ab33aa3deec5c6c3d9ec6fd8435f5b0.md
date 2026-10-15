
## 示例 4-9 使用 `scsi_info -i /dev/sg2` 获取设备信息

```
root@diomede /root# scsi_info -i /dev/sg2

Inquiry command

----

Relative Address     0

Wide bus 32         0

Wide bus 16         0

Synchronous neg.     0

Linked Commands      0

Command Queuing     0

Peripheral               0

Device Type         8

Peripheral Qualifier 0

Removable?          1

Device Type Modifier 0

ISO Version         0

ECMA Version         0

ANSI Version         0

Response Data Format IBM

Vendor: ULT3583-TL

Revision level: 50
```

## 4.3.4 `mtx` 工具

一组名为 `mtx` 的低级驱动工具可用于控制 SCSI 设备，例如自动加载器、磁带转换器、磁带库和磁带机。这些工具还可以报告数据，包括序列号、最大块大小和磁带机信息。它们被设计为脚本备份解决方案的低级驱动，而不是高层接口。在我们的环境中，这组工具对于检查 LTO 磁带库的基本操作非常有用。

从此处下载并安装最新的 `mtx` 版本：
`http://mtx.sourceforge.net/`

软件包以压缩 tar 文件提供，并如示例 4-10 所示进行解压和安装。

## 示例 4-10 解压并安装 `mtx`

```
[root@bonnie /root]# tar xzf mtx-1.23.13.tar.gz

[root@bonnie /root]# cd mtx-1.23.13

[root@bonnie mtx-1.23.13]# /configure

creating cache /config.cache

checking host system type... i686-pc-gnu

checking target system type... i686-pc-gnu

checking build system type... i686-pc-gnu

checking for gcc... gcc

(..)

updating cache /config.cache

creating /config.status

creating Makefile

creating config.h

config h is unchanged
```

```
[root@bonnie mtx-1.23.13]# make

gcc -g2 -DVERSION="1.23.13" -I/usr/src/include

DLONG_REQUEST_SENSE=1 -c -o mtx.o mtx.c

(..)

gcc -g2 -DVERSION="1.23.13" -I/usr/src/include

DLONG_REQUEST_SENSE=1 -c -o scitape.o scitape.c

scitape.c:99: warning: 'PeripheralDeviceType' defined but not used

gcc -o scitape scitape.o mtx.o
```

```
[root@bonnie mtx-1.23.13]# install

for file in mtx tapeinfo scitape; do \

  strip $file; \

  /usr/bin/install -m 755 -d /usr/local/sbin
```

```
/usr/bin/install -c -m 755 mtx tapeinfo scitape /usr/local/sbin

/usr/bin/install -c -m 755 -d /usr/local/man /usr/local/man/man1

/usr/bin/install -c -m 644 mtx.1 tapeinfo.1 scitape.1 loader.1 /usr/local/man
```

可以使用 `mtx` 命令并更近地观察我们的 LTO 磁带库。我们使用 `status` 子命令从 LTO 磁带库获取详细状态信息（参见示例 4-11）。在系统启动后或当磁带放入或取出库时，我们建议使用 `mtx` 的 `inventory` 子命令以确保从 `status` 子命令获取的信息是正确的。

## 示例 4-11 使用 `mtx` 获取磁带库的详细清单

```
bonnie:usr/src/linux # mtx -f /dev/sg2 status

Storage Changer /dev/sg2: Drives, 5 Slots ( 12 Import/Export )

Data Transfer Element 0:Empty

Data Transfer Element 1:Empty

Storage Element 2:Empty

Storage Element 3:Empty

Storage Element 4:Empty

Storage Element 5:Empty

Storage Element 6:Empty

Storage Element 7:Full :VolumeTag=ABA927L

Storage Element 8:Empty

Storage Element 9:Empty

Storage Element 10:Empty

Storage Element 11:Empty

Storage Element 12:Empty

Storage Element 13:Empty

Storage Element 14:Full :VolumeTag=ABA926L

Storage Element 15:Empty

(...)

Storage Element 39:Empty

Storage Element 40:Full :VolumeTag=ABA928L

Storage Element 41:Full :VolumeTag=ABA990L

Storage Element 42:Full :VolumeTag=ABA922L

Storage Element 43: IMPORT/EXPORT:Empty

Storage Element 54: IMPORT/EXPORT:Empty
```

在将磁带移回存储元件之前，我们必须如图 4-13 所示卸载磁带驱动。

示例 4-13 使用 `mt` 从磁带驱动器卸载磁带
```bash
[root@diode /root]# mt -f /dev/stl1 offline
```

最后，我们可以使用 `unload` 子命令将磁带移回它的存储元件（示例 4-14）。

示例 4-14 使用 `mtx` 从磁带驱动器移除磁带
```bash
[root@diode /root]# mtx -f /dev/sg2 unload 41 1

Unloading Data Transfer Element into Storage Element 41...done
```
