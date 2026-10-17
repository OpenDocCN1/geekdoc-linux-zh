
如果处于万不得已，向 `mail-server@rtfm.mit.edu` 发送邮件并在信息中包含“help”，然后按照邮件中的说明操作。

## A.6 Ramdisk 使用

关于新 ramdisk 代码的优秀描述可以在 Linux 内核提供的文档中找到。请参见 `/usr/src/linux/Documentation/ramdisk.txt`。它由 Paul Gortmaker 编写，包含一个创建压缩内存磁盘的章节。

## A.7 Linux 启动过程

关于 Linux 启动过程的详细信息，这里是一些索引：

- 《Linux 管理员》有一个关于启动的章节，参见 `http://sunsite.unc.edu/LDP/sag-0.5/node68.html`
- LILO “技术概览” `<http://sunsite.unc.edu/pub/Linux/system/boot/lilo-t-20.gz>` 提供了权威的技术介绍、启动过程的低级描述以及内核启动的位置。
- 与启动过程相关的内核源码，你可以在机器的 `/usr/src/linux/` 下找到它；此外，`shigio` 在 `<http://wafu.net/>` 拥有一个非常好的超文本浏览器，用于启动区的汇编代码。

## B LILO 错误代码

Usenet 上经常有关于这些错误的问题。我们在这里列出它们，可以参考 Werner Alberger 的文档 `<ftp://sunsite.unc.edu/pub/linux/local/lilo.19.ps.gz>`。

| 错误代码 | 描述 |
| :--- | :--- |
| (nothing) | `LILO` 部分已加载。`LILO` 未安装或其启动区未激活。 |
| L | 第一阶段加载器已加载并启动，但无法加载第二阶段加载器。这种两位数字错误代码通常表示介质失败或几何结构不匹配。 |
| LI | 第一阶段加载器能够加载第二阶段加载器，但执行失败。这通常是由介质失败或几何结构不匹配引起的。 |
| LIL | 第二阶段加载器在错误的地址加载。这通常是由细微的几何结构不匹配引起的。 |
| LIL- | 描述表损坏。 |
| LILO | `LILO` 部分已成功加载。当 `LILO` 尝试加载启动镜像时会显示相应的错误代码。这些代码范围从 `0x00` 到 `0xb`。请参阅 `LILO` 用户指南获取解释。 |

## C 根磁盘列表

这里是 Graham 的根磁盘和工具磁盘的内容。这些列表作为创建可用系统的文件示例。

```
total 18
drwxr-xr-x 2 root root      1024 Jul 29 21:16 bin/
drwxr-xr-x 2 root root      9216 Jul 28 16:21 dev/
drwxr-xr-x 3 root root      1024 Jul 29 20:25 etc/
drwxr-xr-x 2 root root      1024 Jul 28 19:53 lib/
drwxr-xr-x 2 root root      1024 Jul 24 22:47 mnt/
drwxr-xr-x 2 root root      1024 Jul 24 22:47 proc/
drwxr-xr-x 2 root root      1024 Jul 28 19:07 sbin/
drwxr-xr-x 2 root root      1024 Jul 29 20:57 tmp/
drwxr-xr-x 4 root root      1024 Jul 29 21:35 usr/
drwxr-xr-x 3 root root      1024 Jul 28 19:52 var/
```

```
/bin:
total 713
-rwxr-xr-x 1 root bin      7737 Jul 24 22:16 cat*
-rwxr-xr-x 1 root bin      9232 Jul 24 22:48 chmod*
-rwxr-xr-x 1 root bin      8156 Jul 24 22:48 churn*
-rwxr-xr-x 1 root bin     19652 Jul 24 22:48 cp*
-rwxr-xr-x 1 root root      8313 Jul 29 21:16 cut*
-rwxr-xr-x 1 root bin     12136 Jul 24 22:48 dd*
-rwxr-xr-x 1 root bin      9308 Jul 24 22:48 df*
-rwxr-xr-x 1 root root      9036 Jul 29 20:24 discors*
-rwxr-xr-x 1 root bin     9064 Jul 24 22:48 du*
-rwxr-xr-- 1 root bin     69252 Jul 24 22:51 e2fsck*
-rwxr-xr-x 1 root bin     5361 Jul 24 22:48 echo*
-rwxr-xr-x 1 root bin     6596 Jul 24 22:49 kill*
-rwxr-xr-x 1 root bin    10644 Jul 24 22:17 ln*
-rwxr-xr-x 1 root bin     13508 Jul 24 22:17 login*
-rwxr-xr-x 1 root bin     26976 Jul 24 22:49 ls*
-rwxr-xr-x 1 root bin     7416 Jul 24 22:49 mkdir*
-rwxr-xr-- 1 root bin     34596 Jul 24 22:51 mke2fs*
-rwxr-xr-x 1 root root      6712 Jul 24 22:49 mknod*
-rwxr-xr-x 1 root bin     20304 Jul 24 22:17 more*
-rwxr-xr-x 1 root root     24704 Jul 24 22:17 mount*
-rwxr-xr-x 1 root bin     12464 Jul 24 22:17 mv*
-rwxr-xr-x 1 root bin     20829 Jul 24 22:50 ps*
-rwxr-xr-x 1 root bin      9424 Jul 24 22:50 rm*
-rwxr-xr-x 1 root bin      4344 Jul 24 22:50 rmd*
```

## C. 根目录示例列出

```
-rxr-xr-x 1 root bin 9853 Jul 24 22:17 su*
-rxr-xr-x 1 root bin 380 Jul 27 14:12 sync*
-rwxr-xr-x 1 root bin 13620 Jul 24 22:17 umount*
-rwxr-xr-x 1 root root 5013 Jul 29 20:03 uname*
```

### /dev

```
total 0
lrwx-rw-x 1 root root 10 Jul 24 22:34 cdrom -> /dev/sbpcd
crw-w--y- 1 root tty 4, 0 Jul 24 21:49 console
brw-rw-- 1 root floppy 2, 0 Apr 28 19:55 fd0
lrwx-rw-x 1 root root * 4 Jul 24 22:34 ftape -> rft0
crw-rw-- 1 root sys 10, 2 Jul 18 1994 importbm
crw-rw-- 1 root kmem 1, 2 Jul 28 16:21 kmem
crw-rw-- 1 root kmem 1, 1 Jul 18 1994 mem
lrwx-rw-x 1 root root * 4 Jul 24 22:34 modem -> cua0
lrwx-rw-x 1 root root * 4 Jul 24 22:34 modem -> cua1
crw-rw-- 1 root sys 1, 3 Jul 18 1994 null
brw-rw-- 1 root disk 1, 1 Jul 18 1994 ram
brw-rw-- 1 root disk 27, 0 Jul 18 1994 rft0
brw-rw-- 1 root disk 25, 0 Jul 19 1994 sbpcd
*** 我包含了我使用的 SCSI 分区设备。
*** 如果你使用 IDE，请使用 /dev/hddx。
brw-rw-- 1 root disk 8, 0 Apr 29 1995 sda5
brw-rw-- 1 root disk 8, 6 Apr 29 1995 sda6
brw-rw-- 1 root disk 8, 7 Apr 29 1995 sda7
brw-rw-- 1 root disk 8, 8 Apr 29 1995 sda8
```
