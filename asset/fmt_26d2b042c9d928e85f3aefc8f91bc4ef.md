
我们将在本章后面部分介绍设备文件。但为了说明这个示例，只需知道有一个名为`/dev/dsk/c0t3d0s1`的磁盘部分被用作`swap`即可。如`swap -l`所示，有一个名为`s1`的磁盘`c0t3d0`切片被保留用于`swap`。

除了列表和汇总输出外，`swap`还可用于添加和删除`swap`空间。由于这完全是系统管理员的职责范围，因此我不会详细介绍这些选项。

![](img/75f39fc91296b889c0653851accdfd46_809_2.png)

你可以随时使用`mount`命令快速查看已挂载的文件系统。通常用户可以访问此命令以查看已挂载的文件系统；但作为用户，你可能无法以挂载或卸载等方式操作文件系统。我们在书中介绍的大多数命令在不同 UNIX 变体中会产生略有不同的结果。`mount`命令也不例外。以下示例分别展示了在 Solaris、AIX 和 HP-UX 上运行`mount`命令的结果：

![](img/75f39fc91296b889c0653851accdfd46_810_0.png)

```
sunl $ mount
/proc on /proc read/write/setuid on Thu Feb 18 11:09:14
/ on /dev/dsk/c0t3d0s0 read/write/setuid/largefiles on Thu Feb 18 11:09:14
/dev/fd on fd read/write/setuid on Thu Feb 18 11:09:14
/tmp on swap read/write on Thu Feb 18 11:09:16
/opt/local on ptc-nfs:/export/opt/local read/write/intr/soft/remote on Sun Jul 9
sunl $
```

```
ibm1 $ mount
           node    mounted over      mounted over    vfs     date       options
   ----------   ---------------   ---------------  ------  --------  -------------
   /dev/hd4      /                 jfs     Jul 02 19:02  rw,log=/dev/hd8
   /dev/hd2      /usr              jfs     Jul 02 19:02  rw,log=/dev/hd8
   /dev/hd3var   /var              jfs     Jul 02 19:02  rw,log=/dev/hd8
   /dev/hd3      /tmp              jfs     Jul 02 19:02  rw,log=/dev/hd8
   /dev/hd10     /usr/sys/inst.images jfs    Jul 02 19:03  rw,log=/dev/hd8
   /dev/lv00     /opt              jfs     Jul 02 19:03  rw,log=/dev/hd8
   /dev/bakup    /home.bak         jfs     Jul 02 19:03  rw,log=/dev/hd8
   /dev/cd0      /usr/lpp/info/data/techlib cdrfs  Jul 02 19:03  ro
   /dev/lv01     /root/users       jfs     Jul 02 19:03  rw,log=/dev/hd8
   auto.hosts    /net            autoofs Jul 02 19:04  ignore
   auto.users    /users            autoofs Jul 02 19:04  ignore
   auto.ptc      /bpt_mnt          autofs Jul 02 19:04  ignore
   auto.indirect /local_mnt        autofs Jul 02 19:04  ignore
   auto.direct   /home/ptc-nfs     autofs Jul 02 19:04  ignore
   auto.direct   /opt/local        autofs Jul 02 19:04  ignore
   ibm1 $
```

```
hpl 22: mount
/ on /dev/vg00/lvol3 log on Wed Jun 16 11:20:07
/stand on /dev/vg00/lvol1 defaults on Wed Jun 16 11:20:10
/var on /dev/vg00/lvol8 delaylog on Wed Jun 16 11:20:21
/usr on /dev/vg00/lvol7 delaylog on Wed Jun 16 11:20:21
/tmp on /dev/vg00/lvol6 delaylog on Wed Jun 16 11:20:22
/opt on /dev/vg00/lvol5 delaylog on Wed Jun 16 11:20:22
/home on /dev/vg00/lvol4 delaylog on Wed Jun 16 11:20:22
hpl 23:
```

虽然我习惯不展示许多不同 UNIX 变体的命令示例，但我还是决定包含`mount`命令的输出。这是因为这三种输出差异足够大，可以说明尽管提供的一般信息相同，但输出格式却不同。这一事实在系统管理相关命令中尤为明显，这也是 UNIX 变体差异最大的领域。概念是相同的，但文件位置、选项以及当然还有格式可能会有所不同。只要你了解从一个 UNIX 变体到另一个变体之间的这些信息，你只需调整思维以适应命令中可能的变化即可。

大多数 UNIX 变体中，启动时挂载的文件系统位于`/etc/vfstab`或`/etc/fstab`文件中。该文件包含有关待挂载设备、挂载点、文件系统类型、挂载选项以及其他重要挂载信息的内容。你可以查看系统中的此文件，以查看系统管理员设置的默认文件系统。

### 确定磁盘使用情况

![](img/75f39fc91296b889c0653851accdfd46_811_0.png)

系统管理员希望了解用户、应用程序、组等在系统中消耗的磁盘空间量。了解系统中的“磁盘占用大户”是个好主意。`du`命令有助于确定这一点。使用`du`时，你指定一个文件以查看其磁盘使用情况。对于主目录`martyp`，你会发出以下`du`命令：

```
martyp $ du
2 ./test
60 ./shellprogs
1366 ./.trash
6024 .
martyp $
```

此输出显示该目录消耗了 6024 KBytes（约 6 MBytes）。对于包含大量条目的大型目录，这可能产生大量的输出。如果只需要摘要，你可以使用`-s`选项发出`du`命令，并获得整个主目录的以下结果：
