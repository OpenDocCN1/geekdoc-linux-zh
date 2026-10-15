

## FIGURE 4.5 理解 df 输出。

磁盘设备的名称

设备总大小（以 Kbytes 为单位）

已使用的 Kbytes

可用的 Kbytes

使用百分比

文件系统中的挂载点

dev/sd0a 55735 37414 12748 75% /

你可以将列相加可知，系统总共有约 300MB 的磁盘空间（55,735 + 187,195 + 55,688），其中 230MB 已被使用。因此剩余空间为 33MB，占总磁盘大小的 16%。

4. 许多现代 Unix 系统允许你使用带 -h 标志的 du。 （某些 man 手册将其称为人类可读输出标志！）这提供了更有用的输出格式。以下是来自另一台计算机系统的示例：

```
% df
Filesystem      kbytes   used   avail capacity  Mounted
/dev/sd0a       55735    37414  12748   75%    /
/dev/sd2b       187195   153569 14907   91%    /usr
/dev/sd1a       55688    43089  7031    86%    /utils
```

```
% df -h
Filesystem   Size   Used   Avail Capacity  Mounted on
/dev/sd0a    15G    2.1G   13G    14%      /
/dev/sd1a    15G    157M   15G    1%       /web
```

5. Mac OS X 是更现代的 Unix 之一，它在 df 输出中包含了各种非磁盘设备，如本示例所示：

```
$ df -h
Filesystem        Size   Used  Avail Capacity  Mounted on
/dev/disk0s8      49G    43G   6.1G   88%      /
devfs             94K    94K   0B     100%     /dev
fdesc             1.0K   1.0K  0B     100%     /dev
<volfs>           512K   512K  0B     100%     /.vol
automount -nsl [335] 0B 0B 0B 100% /Network
automount -fstab [338] 0B 0B 0B 100% /automount/Servers
automount -static [338] 0B 0B 0B 100% /automount/static
```

在所有这些输出中，系统上实际上只有一个磁盘，/dev/disk0s8，它是一个 49GB 的硬盘，已使用 88%。

6. 尝试在你的系统上使用 du 和 df 命令，以确定整个系统以及你用于主目录的磁盘上可用的磁盘空间。然后使用 du 来识别你的文件和目录占用了多少空间。

## Task 4.12: 使用 `gzip` 程序缩小大文件

现在你可以通过目录中的文件确定你使用了多少空间，你已准备好学习如何在不删除任何文件的情况下节省空间。Unix 有一个内置程序——`gzip` 程序——提供了这种功能。

内置于 Unix 的原始压缩程序称为 `compress`，但现在你可以使用另外两种压缩文件的工具，它们往往做得更好：`gzip` 和 `bzip2`。

- 1. 在这个简单示例中，`gzip` 程序被赋予一个文件名列表，然后压缩每个文件并将其重命名为以 `.gz` 后缀结尾，这表明它们已被压缩：

[Click here to view code image](#)

```
% ls -l LISTDATA2
-rw-r--r-- 1 taylor taylor 24064 23 Apr 22:41 LISTDATA2
% gzip LISTDATA2
% ls -l LIST*
-rw-r--r-- 1 taylor taylor 3682 23 Apr 22:41 LISTDATA2.gz
```

压缩 LISTDATA2 文件使其大小从 24 千字节减少到略多于 3 千字节（磁盘空间节省了近 85%）。如果你预计系统上会有大型文件且不会经常访问，使用 `gzip` 程序可以节省大量磁盘空间。

- 2. 在更大的文件上使用 `gzip` 可以显示更大的节省（请注意，我还添加了 `-v` 标志，它显示了通过对相关文件使用 gzip 所获得的节省程度）：

[Click here to view code image](#)

```
% ls -l big.file
-rwx-- 1 taylor taylor 3198588 23 Apr 22:48 big.file
% gzip -v big.file
big.file: 72.7% - replaced with big.file.gz
% ls -l big.file*
-rwx-- 1 taylor taylor 871440 23 Apr 22:48 big.file.gz
```

这个单一命令能够释放近 3MB 的磁盘空间。如果你使用 PC 运行 Unix，或者你在一个有许多用户（你可以通过使用 `w` 命令轻松确定）的系统上，压缩文件可能需要花费大量时间。

- 3. 要反转此操作，请使用配套命令 `gunzip` 并指定文件的当前名称（即带有 `.gz` 后缀）或文件在压缩前的名称（即不带 `.gz` 后缀）：

```
% gunzip LISTDATA2
% ls -l LISTDATA2
-rw-r--r-- 1 taylor taylor 24064 23 Apr 22:41 LISTDATA2
```

