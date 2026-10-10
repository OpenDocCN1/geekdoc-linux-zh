

# 附录 A 834

## FAT 挂载选项

**conv=b[inary] / conv=t[ext] / conv=a[uto]** *fat* 文件系统可以在内核中执行 CRLF<>NL（MS-DOS 文本格式到 UNIX 文本格式）转换。可用的转换模式如下：

- **binary**：不执行转换。这是默认值。
- **text**：对所有文件执行 CRLF<>NL 转换。
- **auto**：对所有不具有“已知二进制”扩展名的文件执行 CRLF<>NL 转换。已知扩展名的列表可以在 *fs/fat/misc.c* 的开头找到（截至 2.0 版本，列表为：exe, com, bin, app, sys, drv, ovl, ovr, obj, lib, dli, dif, arc, zip, lha, lzh, 2oo, taz, z, arj, tz, taz, tzp, tpz, gz, tgz, deb, gif, bmp, tif, gif, jpg, pcx, tfm, vf, gif, pkl, pxi, dvi）。

执行计算型 lseek 的程序不会喜欢内核内的文本转换。许多人因此而导致数据损坏。请小心！

对于以二进制模式挂载的文件系统，提供了转换工具（fromdos/todos）。

- **debug**：打开调试标志。将打印版本字符串和文件系统参数列表（如果参数似乎不一致，也会打印这些数据）。
- **fat=12 / fat=16**：指定 12 位 fat 或 16 位 fat。这会覆盖自动 FAT 类型检测例程。请谨慎使用！
- **quiet**：打开静默标志。尝试 chown 或 chmod 文件时不会返回错误，尽管它们会失败。请谨慎使用！
- **sys_immutable, showexec, dots, nodots, dotsOK=[yes, no]**：各种试图将 Unix 或 DOS 约定强加于 FAT 文件系统的 misguided（ misguided/误入歧途）尝试。

## HPFS 挂载选项

- **uid=value 和 gid=value**：设置所有文件的属主和组。（默认值：当前进程的 uid 和 gid。）
- **umask=value**：设置 umask（权限缺失的位掩码）。默认值是当前进程的 umask。数值以八进制给出。
- **case=lower / case=asis**：将所有文件名转换为小写，或保持原样。（默认值：case=lower。）
- **conv=binary / conv=text / conv=auto**：对于 conv=text，读取文件时删除一些随机的 CR（特别是那些后面跟着 NL 的）。对于 conv=auto，在 conv=binary 和 conv=text 之间随机选择。对于 conv=binary，仅读取文件中的内容。这是默认值。
- **nocheck**：当某些一致性检查失败时，不中止挂载。

## ISO9660 挂载选项

普通的 iso9660 文件名以 8.3 格式出现（即类似 DOS 的文件名长度限制），此外所有字符都是大写的。也没有用于文件所有权、保护、链接数、块/字符设备等字段。

Rock Ridge 是 iso9660 的扩展，提供了所有这些类 Unix 特性。基本上，每个目录记录都有扩展，提供所有附加信息，当使用 Rock Ridge 时，文件系统与普通的 Unix 文件系统无法区分（当然，它是只读的）。

- **norock**：禁用 RockRidge 扩展的使用，即使可用。参见 map。
- **check=r[elaxed] / check=s[trict]**：当使用 check=relaxed 时，在执行查找之前，文件名会先转换为小写。这通常仅在与 norock 和 map=normal 一起使用时有意义。（默认值：check=strict。）
- **uid=value 和 gid=value**：给文件系统中的所有文件赋予指定的用户或组 ID，可能会覆盖在 Rock Ridge 扩展中发现的信息。（默认值：uid=0, gid=0。）
- **map=n[ormal] / map=o[ff]**：对于非 Rock Ridge 卷，普通的名称转换将大写 ASCII 映射为小写，去掉结尾的 “;1”，并将 “;” 转换为 “.”。当使用 map=off 时，不进行名称转换。参见 norock。（默认值：map=normal。）
- **mode=value**：对于非 Rock Ridge 卷，给所有文件赋予指定的模式。（默认值：所有人可读权限。）自 Linux 2.1.37 起，不再需要以十进制指定模式。（八进制由前导 0 表示。）
- **unhide**：还显示隐藏文件和关联文件。
- **block=[512|1024|2048]**：将块大小设置为指定值。（默认值：block=1024。）
- **conv=[auto|b|binary|m|text|t|txt]**：（默认值：conv=binary。）自 Linux 1.3.54 起，此选项无效。（并且非二进制设置曾经非常危险，通常会导致静默数据损坏。）
- **cruft**：如果文件长度的高字节包含其他垃圾数据，设置此挂载选项以忽略文件长度的高位。这意味着文件不能大于 16Mb。如果整个 CDROM 具有异常大小（负值或大于 800MB），cruft 选项会自动设置。当看到除 0 或 1 以外的卷序列号时，也会设置此选项。

## MINIX 挂载选项

无。

## MS-DOS 挂载选项

参见 FAT 的挂载选项。如果 msdos 文件系统检测到不一致性，它会报告错误并将文件系统设置为只读。可以通过重新挂载文件系统使其再次变为可写。

## NCP 挂载选项

就像 nfs 一样，ncp 实现期望挂载系统调用有一个二进制参数（a struct ncp_mount_data）。该参数由 ncpmount(8) 构造，当前版本的 mount (2.6) 不了解 ncp。

## NFS 挂载选项

内核解析的不是文本选项字符串，nfs 文件系统期望一个类型为 struct nfs_mount_data 的二进制参数。mount 程序本身解析以下 'tag=value' 形式的选项，并将它们放入上述结构中：size=n, wsize=n, timeo=n, retrans=n, acregmin=n, acregmax=n, acdirmin=n, acdirmax=n, actimeo=n, retry=n, port=n, mountport=n, mounthost=name, mountprog=n, mountvers=n, nfsprog=n, nfsvers=n, namlen=n。选项 add=n 被接受但被忽略。还识别以下布尔选项（可能前面带有 no）：bg, fg, soft, hard, intr, posix, cto, ac, tcp, udp, lock。详情参见 nfs(5)。

特别有用的选项包括：

- **rsize=8192, wsize=8192**：这将使您的 nfs 连接比默认缓冲区大小 1024 快得多。
- **hard**：访问 NFS 挂载文件系统中文件的程序将在服务器崩溃时挂起。除非您也指定了 intr，否则进程不能被中断或杀死。当 NFS 服务器重新上线时，程序将从中断处继续运行而不受干扰。这很可能是您想要的行为。
- **soft**：此选项允许内核在 nfs 服务器一段时间无响应时超时。时间可以用 timeo=time 指定。如果您的 nfs 服务器有时无响应或当某个进程试图从服务器获取文件时服务器将重启，此选项可能有用。通常它只会带来很多麻烦。
- **nolock**：不使用锁定。不启动锁定。

## PROC 挂载选项

**uid=value 和 gid=value**：据我观察，这些选项被识别，但没有效果。

## ROMFS 挂载选项

无。

## SMBFS 挂载选项

就像 nfs 一样，smb 实现期望挂载系统调用有一个二进制参数（a struct smb_mounter_data）。该参数由 smbmount(8) 构造，当前版本的 mount (2.6c) 不了解 smb。

## SYSV 挂载选项

无。

## UFS 挂载选项

无。

## UMSDOS 挂载选项

参见 ms-dos 的挂载选项。**dotsOK** 选项被 umsdos 显式禁用。

## VFAT 挂载选项

首先，识别 *fat* 的挂载选项。**dotsOK** 选项被 *vfat* 显式禁用。此外，还有：

- **uni_xlate**：将未处理的 Unicode 字符转换为特殊转义序列。这允许您备份和恢复使用任何 Unicode 字符创建的文件名。如果没有此选项，当无法转换时使用 `?`。转义字符是 `':'`，因为在 vfat 文件系统中它是非法的。使用的转义序列为，其中 *u* 是 unicode 字符：`':'`, (u & 0x3f), ((u>>6) & 0x3f), (u>>12)。
- **posix**：允许两个仅在大写/小写上有区别的文件名。
- **nonumtail**：首先尝试创建不带序列号的短文件名，然后再尝试 *name*`~`*num.ext*。

## XENIX 挂载选项

无。

## XIAFS 挂载选项

无。虽然 xiafs 没有任何问题，但它很少被使用，且不再维护。可能不应该使用它。自 Linux 版本 2.1.21 起，xiafs 不再是内核源代码的一部分。

## 回环设备

另一种可能的类型是通过回环设备挂载。例如，命令

```
mount /tmp/fdimage /mnt -t msdos -o loop=/dev/loop3,blocksize=1024
```

将设置回环设备 */dev/loop3* 以对应文件 */tmp/fdimage*，然后将此设备挂载在 */mnt* 上。这种挂载类型了解三个选项，即 **loop**、**offset** 和 **encryption**，它们实际上是 *losetup*(8) 的选项。如果没有明确指定回环设备（但给出了选项 `-o loop`），则 *mount* 将尝试查找一些未使用的回环设备并使用它。

