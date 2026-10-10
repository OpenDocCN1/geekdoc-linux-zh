

- 将工作目录更改为根目录（/）。
- 将 PATH 设置为 /usr/bin:/usr/sbin:/sbin。
- 更新所有超级块。
- 通知用户已发出关机指令，并要求他们注销。
- 执行 /sbin/rc，执行诸如通过关机脚本（例如 spooler 和 CDE）关闭子系统、卸载文件系统以及其他此类任务。
- 如果使用 -r 选项，则执行 /sbin/reboot。

若要关机并自动重新启动系统，请输入：

```
shutdown -r
```

若要停止系统，请输入：

```
shutdown -h
```

系统将询问您是否希望输入一条消息给用户，告知他们即将进行的系统关机。在您输入消息后，它会立即发送给所有用户。在指定时间过去之后（默认值为 60 秒），系统将开始关机过程。一旦您收到系统已停止的消息，您就可以关闭所有系统组件的电源。

若要在两分钟内关机且不询问任何问题或发送任何消息，请输入：

```
shutdown -h -y 120
```

有时，您需要使用 shutdown 进入单用户模式以执行某些任务（例如备份或扩展逻辑卷），然后重新启动系统以恢复其原始状态。

若要使系统进入单用户模式关机，请输入：

```
shutdown
```

不带任何选项的 **shutdown** 命令会将您带入单用户模式。在操作系统的旧版本中，您可以使用带 *s* 选项的 **init** 命令（**init s**）进入单用户模式。但是，这种做法强烈不推荐，因为该命令不会终止其他系统活动，也不会注销用户；因此，它不会导致真正的单用户状态。

如果系统已经处于单用户模式，或者您喜欢冒险，您可以执行 /usr/sbin/reboot。我强烈建议您执行 **shutdown**，它将调用 **reboot**。**reboot** 命令会突然终止所有进程，然后停止或重新启动系统。此外，在使用动态加载的内核模块时，**reboot** 不会加载这些模块；只有 **shutdown** 会加载。

再次强调，我推荐使用 **shutdown** 命令，而不是 **reboot**。

## 第 9 章

## 文件系统

### 虚拟分区文件系统

每个虚拟分区都有自己的完整 HP-UX 文件系统，就像在单独的服务器上拥有不同的文件系统一样。这些文件系统完全独立运行。如果您希望共享两个 vPar 之间的文件系统信息，您将使用与在服务器之间共享文件系统信息相同的方法，例如网络文件系统（NFS）。不同 vPar 文件系统之间的这种完全独立性确保了 vPar 的完全软件隔离。

在下一节中，我们将涵盖一些与 vPar 文件系统相关的主题，然后是在本章节非 vPar 特定部分中的文件系统背景知识。

### 独立的 vPar 文件系统

vPar 的文件系统在不同的两个 vPar 上会有所不同，就像在两个不同的服务器上会有所不同一样。这意味着在一台服务器上运行的两个 vPar 所占用的磁盘空间可能正好是同一台服务器上运行一个标准 HP-UX 所占用的磁盘空间的两倍。这两个 vPar 中的每一个都需要自己的操作系统、应用程序、用户主目录等。由于除了通常在网络环境中共享的 NFS 文件系统之外，没有任何文件系统被共享，这可能会使您的存储需求翻倍。让我们看一下在两个不同的 vPar 上运行的文件系统。

以下是在服务器上运行的第一个 vPar（主机名 **actappd1**）上运行的 **bdf** 命令结果：

```
# hostname
actappd1
# bdf
Filesystem             kbytes   used    avail  %used Mounted on
/dev/vg00/lvol3        245760 40769 192184   18% / 
/dev/vg00/lvol1        111637 74350 26123    74% /stand
/dev/vg00/lvol8        1732608 598033 1063751 36% /var
/dev/vg00/lvol7        1732608 755560 915987 45% /usr
/dev/vg00/lvol1        1228800 466678 714321 40% /usr1
/dev/vg00/lvol14       258048 69857 174676   28% /tmp
/dev/vg00/lvol16       1531904 1381306 141226 91% /opt
/dev/vg00/lvol5        819200 176605 603031 23% /home
```

此列表显示了 **vg00**，即系统上配置的唯一一个卷组，以及每个逻辑卷中的容量设置。

**接下来**是在服务器上运行的第二个 vPar（主机名 **ecvpar2**）上运行的 **bdf** 命令结果：

```
# hostname
actappd1
# bdf
Filesystem             kbytes    used     avail  %used Mounted on
/dev/vg00/lvol3        143360   43174   93951  31% / 
/dev/vg00/lvol1        111637   73632   26861  73% /stand
/dev/vg00/lvol8        1536000  965183  535326  64% /var
/dev/vg00/lvol7        1593444  740649  799344  48% /usr
/dev/vg00/lvol14       258048   68619   177641  28% /tmp
/dev/vg00/lvol16       2084864  563709  1426107 28% /opt
/dev/vg00/lvol5        819200   1314    766771 0% /home
```

您可以从这两个列表中看出，这两个 **vg00** 卷组所占用的空间大约是不运行 vPar 时所占用的空间的两倍。通过运行两个 vPar，您在这台服务器上很可能完成两倍的工作量，因此这很可能是值得花费的磁盘空间；但是，您需要将其消耗的空间作为规划的一部分来考虑。

我们前面列出的第一个 vPar 也在其上运行了几个应用程序。其中一个是 **BroadVision**，它需要自己在 **/opt/bs** 下的目录，如下面的列表所示：

```
# hostname
actapp01
# ll /opt
total 32
dr-xr-xr-x 7 bin bin 96 Jul 13 15:27 Migration
dr-xr-xr-x 9 bin bin 1024 Jul 13 15:26 OV
drwxrwxr-x 18 bin bin 1024 Jul 13 15:23 apche
dr-xr-xr-x 6 bin bin 96 Jul 13 15:12 asx
dr-xr-xr-x 6 bin bin 96 Jul 13 15:24 audio
drwxr-xr-x 22 root bin 1024 Sep 21 13:34 bvto1
drwxr-xr-x 8 root users 1024 Jul 13 15:26 cifsclient
dr-xr-xr-x 4 bin bin 96 Jul 13 15:26 cmcluster
dr-xr-xr-x 4 bin bin 96 Jul 13 15:25 cmom
dr-xr-xr-x 10 bin bin 1024 Jul 13 15:10 dce
dr-xr-xr-x 4 bin bin 1024 Jul 13 15:35 dcelocal
dr-xr-xr-x 4 bin bin 96 Jul 13 15:13 dmi
dr-xr-xr-x 4 bin bin 96 Jul 13 15:11 fcmo
dr-xr-xr-x 4 bin bin 96 Jul 13 15:17 graphics
dr-xr-xr-x 3 bin bin 96 Jul 13 15:08 gprarray
dr-xr-xr-x 3 bin bin 96 Jul 13 15:14 ior
dr-xr-xr-x 16 bin bin 1024 Jul 19 15:03 ignite
dr-xr-xr-x 3 bin bin 96 Jul 13 15:14 image
dr-xr-xr-x 4 bin bin 96 Jul 13 15:25 java1.2
drwxrwxrwx 7 bin bin 1024 Aug 24 16:34 java1.3
drwxr-xr-x 2 root root 96 Jul 13 15:04 lost+found
dr-xr-xr-x 7 root sys 96 Aug 27 17:26 make
dr-xr-xr-x 8 root sys 1024 Jul 13 15:27 motd
dr-xr-xr-x 9 bin bin 1024 Jul 13 15:26 netscape
dr-xr-xr-x 7 bin bin 96 Jul 13 15:09 nettladm
dr-xr-xr-x 2 bin bin 96 Jul 13 15:11 networkdocs
dr-xr-xr-x 2 bin bin 96 Jul 13 15:16 pamrg
dr-xr-xr-x 7 bin bin 96 Jul 13 15:15 pd
dr-xr-xr-x 12 root bin 1024 Jul 13 15:25 perf
dr-xr-xr-x 9 bin bin 1024 Jul 13 15:26 prn
dr-xr-xr-x 4 bin bin 96 Jul 13 15:11 rai0d48i
dr-xr-xr-x 6 bin bin 96 Jul 13 15:12 reason
drwxr-xr-x 10 root users 1024 Jul 13 15:25 samba
dr-xr-xr-x 3 root users 96 Jul 13 15:24 samba_sro
dr-xr-xr-x 8 bin bin 1024 Jul 13 15:16 scr
dr-xr-xr-x 3 root bin 96 Aug 24 13:42 tiomli
drwxrwxr-x 11 bin bin 1024 Jul 13 15:24 tocsat
dr-xr-xr-x 5 bin bin 96 Jul 13 15:25 tocmate
dr-xr-xr-x 4 bin bin 96 Jul 13 15:25 videod
dr-xr-xr-x 6 bin bin 96 Jul 13 15:26 webadmin
dr-xr-xr-x 10 bin bin 1024 Jul 13 15:27 wlm
#
```

**/bv1to1** 目录是加载 Broadvision 应用程序的目录。此目录将出现在需要运行 Broadvision 的每个 vPar 上。下面的列表显示了使用 du 命令时 /opt 下每个目录所占用的容量：

```
# hostname
actappdi
# cd /opt
# hostname
actappdi
# pwd
/opt
# du -s *
13842 Migration
80456 OV
57604 apache
250 asx
1912 audio
1402052 bv1to1 <-- Broadvision 目录
5072 cifsclient
2304 cmcluster
4720 cmon
22214 dce
2 dcelocal
446 dmi
296 fcms
620 graphics
44848 gparay
28709 isor
146206 ignite
2064 image
136598 java1.2
136910 java1.3
0 lost+found
2386 make
53634 mx
54444 netscape
2292 netiladm
512 networkdocs
1076 parmgr
35770 pd
216234 perf
112774 pvm
2182 raid4ei
850 resmon
26874 samba
10514 samba_src
8648 scr
87810 tivo1i
8628 tomcat
1998 upgrad
1272 video
28684 webadmin
5908 wlm
#
```
