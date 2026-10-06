
与性能有关。使用某些参数可能是危险的。因此，在在使用它时你应该应该小心。

## Modinfo

`modinfo` 命令用于列出 Linux 内核模块的信息。例如，你必须使用 `modinfo cdrom` 命令来获取 CDROM 相关的内核模块信息。

```
root@kemal:~# modinfo cdrom
filename: /lib/modules/4.0.0-kalil-686-pae/kernel/drivers/cdrom.ko
license: GPL
depends:
intro:
vermag: 4.0.0-kalil-686-pae SMP mod_unload versions 686
parm: debug:autoclose
parm: autoeject:bool
parm: lockdoor:bool
parm: check_media_type:bool
parm: mrw_format_restart:bool
```

如果你想查看模块列表，可以使用 `lsmod` 命令。

## Stat

使用 `stat` 命令可以获取文件或目录的状态信息。它可以不带参数使用，也可以带有 `-f` 参数（如 `stat -f`）。

```
root@kemal:~# stat /etc
File: "/etc" Blocks: 24 10 Block: 4096 dizin
Size: 12288 Device: 801/2649d Inode: 17006069 Links: 179
Access: [0755/drwxr-xr-x] Uid: 0/root Gid: 0/root)
Access: 2015-11-12 16:52:11.8637477 +0200
Modify: 2015-11-12 16:17:52.22489130 +0200
Change: 2015-11-12 16:17:52.22489130 +0200
Birth:
root@kemal:~# stat -f /etc
File: "/etc"
ID: c6233bcc30090ee Name: 255 Type: ext2/ext3
Block size: 4096 Fundamental block size: 4096
Blocks: Total: 9327789 Free: 702615 Available: 6547025
Inodes: Total: 2379216 Free: 2027069
```

## Vinstat

我们可以使用 `vmstat` 命令查看系统的整体状态。

```
root@kemal:~# vmstat
procs    memory------swap------system------cpu----
  r b swpd free buff cache  si bo in in cs us sy id wa st
  0 0 263432 11796 15652 232344   0  17  62 27 88 227  4 1 193  2  0
root@kemal:~#
```

如果调用时不带任何参数，信息将在列出后就会退出。为了以特定的时间间隔刷新信息，`vmstat` 命令 应该使用 `vmstat delay [renewal_number]`。

```
root@kemal:~# vmstat 3 4
procs    memory------swap------system------cpu----
  r b swpd free buff cache  si bo in in cs us sy id wa st
  0 0 20568 10580 16528 234484   5 17 62 27 89 231  4  1 193  2  0
  0 0 20568 10324 16628 234804   0  0  0  0 66 163  1 196  2  0
  0 0 20568 10324 16636 234768   0  0  0 13 61 142  1 295  2  0
  0 0 20568 10332 16636 234768   0  0  0  0 178 415  6 9 84  1  0
root@kemal:~#
```

## History

事实上，这个主题可以在后续章节中描述。但在这里提到会更合适。Linux 系统使用的命令保留在内存中（通过为分配的数量的空间写入文件），然后通过调查使用了哪些命令，并让我们追溯允许让我们再次使用它们。是的，命令行中使用的命令保存在 `.bash_history` 文件中。我们可以使用 `history` 命令来列出之前使用的命令。该命令将引用 `.bash_history` 文件。

```
root@kemal:~# history
1 nano /etc/hostname
2 ls
3 tar -zxvf LibreOffice_5.0.0_Linux_x86_deb.tar.gz
4 ls
5 tar -zxvf LibreOffice_5.0.0_Linux_x86_deb_helpack_tr.tar.gz
6 tar -zxvf LibreOffice_5.0.0_Linux_x86_deb_langpack_tr.tar.gz
7 ls
8 cd LibreOffice_5.0.5_Linux_x86_deb
9 ls
10 cd DEBS/
11 ls
12 dpkg -i *.deb
13 ls
14 cd LibreOffice_5.0.5_Linux_x86_deb -h
15 cd LibreOffice_5.0.5_Linux_x86_deb_helpack_tr/
```

要从终端再次使用这些命令列出的命令中的某一个，只需要在命令左侧加上一个 `!` 符号即可。例如，我列出了我在终端编号为 215 的屏幕命令：`cd /home` 命令，为了再次使用它，我必须输入 `!215` 命令。

```
root@kemal:~# !215
cd /home
root@kemal:/home# 
```

如果你想复用最后使用的命令，你必须输入命令 `!!` 来为此

```
root@kemal:~# !!
cd
root@kemal:~#
```

若要以相同的方式使用之前过的命令，应该在命令左侧放置 `!` 符号。例如，如果你想以相同的方式使用 `cat` 命令，你必须输入 `!cat` 命令。

```
root@kemal:~# !cat
cat /proc/meminfo
MemTotal:       502812 kB
MemFree:        19420 kB
MemAvailable:   173512 kB
Buffers:        16596 kB
Cached:         211156 kB
SwapCached:     18876 kB
```

如果你想知道之前使用的命令用法，必须保留关于需要写入终端命令 `<Command>:p` 的说明。因此，它将打印到表单以显示之前使用的命令。

```
root@kemal:~# !cat:p
cat /proc/meminfo
root@kemal:~#
```

如果你想知道之前使用的命令用法，必须保留关于需要写入终端命令 `<Command>:p` 的说明。因此，它将打印到表单以显示之前使用的命令。

如果你想知道之前使用的命令用法，必须保留关于需要写入终端命令 `<Command>:p` 的说明。因此，它将打印到表单以显示之前使用的命令。

如果你想知道之前使用的命令用法，必须保留关于需要写入终端命令 `<Command>:p` 的说明。因此，它将打印到表单以显示之前使用的命令。

如果你想知道之前使用的命令用法，必须保留关于需要写入终端命令 `<Command>:p` 的说明。因此，它将打印到表单以显示之前使用的命令。

如果你想知道之前使用的命令用法，必须保留关于需要写入终端命令 `<Command>:p` 的说明。因此，它将打印到表单以显示之前使用的命令。

如果你想知道之前使用的命令用法，必须保留关于需要写入终端命令 `<Command>:p` 的说明。因此，它将打印到表单以显示之前使用的命令。

（注：原文后续存在大量重复段落，已按要求不重复输出原文）
