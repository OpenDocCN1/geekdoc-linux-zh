
BusyBox 具有高度的模块化和可配置性。虽然它能够实现 300 多个 shell 命令，但你并不需要在系统中包含所有这些命令。配置过程允许你精确选择要包含在系统中的具体命令。表 14.1 列出了近期版本 BusyBox 中可用的完整命令列表。

### 表 14.1：BusyBox 命令

| | | | | | |

|---|---|---|---|---|---|

| acpid | dirname | hwclock | md5sum | resize | tac |

| addgroup | dmesg | id | md | rm | tail |

| adduser | dnsd | ifconfig | mesg | rmdir | tar |

| adjtimex | dnsdomainname | ifenslave | micromcom | rmmod | taskset |

| ar | dos2unix | ifplugd | mkdir | route | tcpdsvd |

| arp | dpkg | inetd | mkdosfs | rpm | tee |

| arping | dumpkmap | init | mknode | run-parts | telnet |

| ash | dumpleases | echo | inotifyd | runlevel | tftp |

| awk | ed | insmod | mkpasswd | runsv | tftp |

| basename | egrep | install | mkswap | rx | time |

| beep | eject | ionice | mktemp | script | timeout |

| blkid | env | ip | mdprobe | scriptreplay | top |

| brctl | envdir | ipaddr | more | sed | touch |

| bunzip2 | envuidgid | ipcalc | mount | sendmail | tr |

| bzcat | expand | ipcrm | mountpoint | setarch | traceroute |

| bzip2 | expr | ipcs | mt | setarch | true |

| cal | fakeidentd | ipink | mv | setconsole | tty |

| cat | false | iproute | nameif | setfont | tysize |

| chat | fbsplash | iprule | nc | setkeycodes | udhcpc |

| chattr | fdflush | iptunnel | netstat | setlogcons | udhcpd |

| chgrp | fdformat | kbd_mode | nice | setstd | udpsvd |

| chmod | fdisk | kill | nmeter | setuidgid | umount |

| chown | find | killall | nohup | sh | uname |

| chpasswd | findfs | killall5 | nsl lookup | openvt | uncompress |

| chpst | flash_lock | klogd | last | sha1sum | unexpand |

| chroot | flash_unlock | length | passwd | sha256sum | uniq |

| chvt | fold | less | path | sha512sum | unixdos |

| ckmount | free | linux32 | pgetch | showkey | unzip |

| clear | free | linux64 | pidof | slattach | uudecode |

| cmp | fsk | linuxrc | ping | sfdelim | uptime |

| comm | fsk_minix | ln | ping6 | sort | usleepp |

| cp | fsync | loadfont | pipe_progress | splkit | uudecode |

| cpio | ftp | loadmap | pivot_root | start-stop-daemon | uuencode |

| crond | ftpget | logger | stat | vi | uconv |

| crontab | ftpput | login | string | su | uconfig |

| cryptpw | fuser | login | printenv | sulogin | watch |

| cut | getty | lotsetup | ps | sum | watchdog |

| date | grep | lpd | pscan | sv | wc |

| dc | gunzip | lpq | pwd | svlogd | wget |

| dd | gzip | lpr | raidautorun | swapoff | which |

| deallocvt | hd | ls | rdote | swapon | who |

| delgroup | hdparm | lattr | rdev | switch_root | whoami |

| deluser | head | lsmode | readlink | sync | xargs |

| depmod | hddump | lzmacat | readprofile | sysctl | yes |

| devmem | hostid | lzop | reaptph | syslogd | zcat |

| df | hostname | lzopcat | reformime | | zip |

| dhcreplay | httpd | makernime | renice | | |

| diff | hush | man | reset | | |

BusyBox 支持 `xconfig` 和 `menuconfig` make 目标用于配置，就像内核一样。图 14.1 展示了 `xconfig` 菜单，而图 14.2 展示了顶级 `menuconfig` 菜单。同样，就像内核一样，还有一个 `make help` 目标，用于列出其他 make 目标。奇怪的是，`xconfig` 并不在该列表中显示。

只有少数几个 `*_defconfig` 目标用于创建默认配置，遗憾的是它们都不匹配 BeagleBone Black。我未能找到 BBB 的默认配置，因此我们有点无所适从。让我们看看如果直接创建一个新配置会发生什么。

## BusyBox 设置

尽管 xconfig 导航面板显示了多个选项类别，但实际上只有两个：配置、构建和安装 BusyBox 的选项，以及选择所需小工具的选项。在 `Build Options` 构建选项中，你可以选择使用静态链接库或共享库来构建 BusyBox。静态链接的 BusyBox 可执行文件要大得多，但你不需要共享库。例如，使用共享库构建的 BusyBox 大小为 743 kb。静态链接版本为 1.5 MB。但是，存放共享库的 `/lib` 目录总共增加了 17 MB。因此问题变成了：你是否还需要这些共享库用于其他用途？

在构建选项 `Build Options` 中，你还可以设置交叉编译器前缀。将其设置为 `arm-linux`...

在 `Installation Options` 安装选项中，你可以选择如何创建符号链接。它们可以是软链接、硬链接或脚本“包装器”。旁边的框解释了硬链接和软链接之间的区别。由于指向相同数据的硬链接共享同一个 inode，这在 inode 数量有限的系统上可能是一个有用的选项。软链接是默认设置，通常也是最佳选择。

## qconf

![](img/f03d6fa2c5faefc793771df52bbb2ef9_228_0.png)

> **缓冲区分配策略**
>
> BusyBox 处理缓冲区分配有 3 种方式：
>
> - 使用 `malloc`。这会因调用 `xmalloc` 而增加代码大小。
> - 将其放在栈上。对于一些栈空间非常有限的微型机器，这可能是致命的。对大多数人来说，这样工作得很好。
> - 将其放在 `BSS` 中。对于拥有真实 `MMU` 和操作系统支持的计算机，这工作得非常好，但对于 `uClinux`，它会浪费运行时 RAM。这种行为是 BusyBox `0.48` 及更早版本唯一可用的行为。

### 图 14.1

BusyBox `xconfig` 菜单。
