
应该使用 `whereis` 命令来查找资源文件和帮助文件的位置。在不带参数使用时，它会将可执行文件和数据的位置输出到帮助页面。如果我们在命令中带有 `-b` 参数，它将只显示可执行文件的位置；使用 `-m` 则只显示手册页（man page）的位置；使用 `-s` 则显示其存在的位置信息。

```
root@kemal:~# whereis ls
ls: /bin/ls /usr/share/man/man1/ls.1.gz
root@kemal:~# whereis -b ls
ls: /bin/ls
root@kemal:~# whereis -m ls
ls: /usr/share/man/man1/ls.1.gz
root@kemal:~# whereis -s ls
ls:
```

## Which

`which` 命令用于找到作为命令参数的命令信息的完整路径。

```
root@kemal:~# which cat
/bin/cat
root@kemal:~# _
```

## Locate

通过此命令，我们可以找到文件所在的位置——即在哪个目录下。例如，让我们查找名为 `.conf` 文件的系统配置文件，我们正在 `/etc` 目录下查找文件。大多数配置文件都在这个目录下。为此，我们需要使用 `locate conf | grep /etc` 命令。

```
root@kemal:~# locate conf | grep /etc
/etc/adduser.conf
/etc/apg.conf
/etc/arpwatch.conf
/etc/avrdude.conf
/etc/ca-certificates.conf
/etc/chkrootkit.conf
/etc/dconf
/etc/debconf.conf
/etc/deluser.conf
/etc/dyleyna-server-service.conf
/etc/dns2tcpd.conf
/etc/foremost.conf
/etc/fragroute.conf
/etc/fuse.conf
/etc/gai.conf
/etc/gconf
/etc/gssapi.conf
/etc/hdparm.conf
/etc/host.conf
```

## Didecode

可以使用 `dmidecode` 命令查看有关 BIOS 的系统硬件组件信息。这些信息通过读取系统 "DMI"（桌面管理接口）获取，该命令的通用用法带有 `-t` 参数：

- 系统 `system`
- 主板 `baseboard`
- 机箱 `chassis`
- 处理器 `processor`
- 内存 `memory`
- 缓存 `cache`
- 连接器 `connector`
- 槽位 `slot`

例如 `dmidecode -t system`：

```
root@kemal:~# dmidecode -t system
SMBIOS 2.4
Handle 0x0001, DMI type 1, 25 bytes
System Information
Manufacturer: Hewlett-Packard
Product Name: Compaq nx6110
Version: F484
Serial Number: CNU0010
UUID: ECC5280-CA62-DA90-A106129
Wake-up Type: Power Switch
Status: No errors detected
```

如果你想查看 CPU 信息，应该使用 `dmidecode -t 4`。

```
root@kemal:~# dmidecode -t 4
SMBIOS 2.4
Handle 0x0004, DMI type 4, 35 bytes
Processor Information
Socket Designation: CPU1
Type: Central Processor
Family: Pentium M
Manufacturer: Intel (R)
ID: 06 00 FF E9
Signature: Type 0, Family 6
```

## 从 `/proc` 文件系统获取信息

关于关于 CPU 和 RAM 的更详细信息，可以使用 `proc` 虚拟文件系统。对于 CPU，`cat /proc/cpuinfo`；对于内存，`cat /proc/meminfo` 会返回我们所需的信息。

```
root@kemal:~# cat /proc/cpuinfo
processor : 0
vendor_id : GenuineIntel
cpu family : 6
model : 13
model name : Intel(R) Celeron(R) M processor
stepping : 8
microcode : 0x20
cpu MHz : 1496.302
cache size : 1024 KB
```

```
root@kemal:~# cat /proc/meminfo
MemTotal: 502812 kB
MemFree: 22784 kB
MemAvailable: 128436 kB
Buffers: 3220 kB
Cached: 180316 kB
SwapCached: 33832 kB
Active: 240760 kB
Inactive: 193188 kB
Active(anon): 166256 kB
```

## Fdisk -l

实际上，如果你使用带有 `-l` 参数的 `fdisk` 命令对磁盘进行分区，你可以通过 `fdisk` 查看系统上的磁盘分区。

```
root@kemal:~# fdisk -l
Disk /dev/sda: 37,3 GiB, 4000776120 bytes
Units: sectors of 512 = 512 bytes
Sector size (logical/physical): 512 bytes
I/o size (minimum/optimal): 512 bytes
Disklabel: dos
Disk identifier: 0x85a4e5a1
Device     Start         End Sectors Size Type
/dev/sda       2048 74219519 74217472 35G Linux
/dev/sda2   74219520 78139921 3920401 9G Extended
/dev/sda3   78139922 78177354 37432G Linux
Disk /dev/sdb: 955,5 MiB, 101943688 bytes
Units: sectors of 512 = 512 bytes
Sector size (logical/physical): 512 bytes
I/o size (minimum/optimal): 512 bytes
Disklabel: dos
```

## Df

我们可以通过 `df` 命令学习关于磁盘使用的详细信息。

```
root@kemal:~# df
Filesystem     1K-block Used Use% Mounted on
udev             10240 0 10240 0% /dev
tmpfs             100564 9148 94116 10% /run
/dev/sda         ext4     36394704 9068272 2546012 27% /
tmpfs            tmpfs     251404 256 251148 1% /dev/shm
tmpfs            tmpfs      5120 0 5120 0% /run/lock
tmpfs            tmpfs     251404 0 251404 0% /sys/fs/cgroup
tmpfs            tmpfs      50284 8 50276 1% /run/user/132
tmpfs            tmpfs      50284 32 50252 1% /run/user/0
```

为了获得整理输出（MB, GB），使用了 `df -h` 命令。
