
`checkhomes.sh`: 50.4% -- replaced with `checkhomes.sh.gz`

`checkpwp.sh`: 38.8% -- replaced with `checkpwp.sh.gz`

`delete.sh`: 43.7% -- replaced with `delete.sh.gz`

```
DEMO/testfile:               0.0% .. replaced with DEMO/testfile.gz
DEMO/Src/cribbage.c:         69.0% .. replaced with DEMO/Src/cribbage.c.gz
DEMO/snapshot.sh:            28.8% -- replaced with DEMO/snapshot.sh.gz
DEMO/sourcefiles.cpio:       72.8% -- replaced with DEMO/sourcefiles.cpio.gz
diskhogs.sh:                 37.2% -- replaced with diskhogs.sh.gz
getmodemdriver.sh:           37.0% -- replaced with getmodemdriver.sh.gz
getstocks.sh:                39.1% -- replaced with getstocks.sh.gz
gettersheet.sh:              37.0% -- replaced with gettersheet.sh.gz
rowing-w-jasmine2.jpg:        0.2% .. replaced with rowing-w-jasmine2.jpg.gz
suspend.sh:                  47.3% -- replaced with suspend.sh.gz
```

![](img/5ced0c78d748bd190e9027e5549a3622_157_0.png)

> 如果你之前没见过，`~acct`记法是用户`acct`主目录的便捷快捷方式。如果未指定任何账户，`~`本身在几乎所有有价值的`shell`中都会扩展为你的主目录。

`gzip`程序已自动将目录（及其下方的子目录）中的每个文件替换为压缩版本，并且如常，每个文件都加上了`.gz`后缀。

这种行为对系统管理员来说非常棒。特别是，当账户被挂起时，这可以是一个很好的额外步骤——自动压缩用户主目录中的所有文件，以最大化活跃用户的可用磁盘空间。

- 4. `gunzip`命令是通过硬链接的`gzip`程序的另一个名称。符号链接与硬链接的细微差别有点超出本书范围（请查看 Sams Teach Yourself Unix in 24 Hours 以获得良好解释），但当你看到类似`gzip`（带命令列表）的`man`手册页开头时，这意味着文件系统以某种方式设置。

因为确保命令正确安装是重要的系统管理员任务，让我们快速插一段来学习这是如何完成的！而且，我喜欢这些插曲，你呢？

```
$ man gzip | head
GZIP(1)                                                                 GZIP(1)

NAME
gzip, gunzip, zcat - compress or expand files

SYNOPSIS
gzip [ -acfhlLnNrtvV19 ] [ -S suffix ] [ name ... ]
gunzip [ -acfhlNrtvV ] [ -S suffix ] [ name ... ]
zcat [ -f hLV ] [ name ... ]
```

![](img/5ced0c78d748bd190e9027e5549a3622_157_1.png)

任何时候你在`man`手册页的`SYNOPSIS`中看到一组不同的命令名称，这意味着同一个可执行二进制文件在文件系统中有多个名称。

这应该可以用`ls`来揭示：

```
$ which gzip
/bin/gzip
$ cd /bin
$ ls -l gzip gunzip zcat
-rwxr-xr-x 3 root root 51228 Aug 23 20:02 gunzip*
-rwxr-xr-x 3 root root 51228 Aug 23 20:02 gzip*
-rwxr-xr-x 3 root root 51228 Aug 23 20:02 zcat*
```

完美。它们大小都相同，并且三个的链接计数也相同（`-l`长输出格式的第二列）。

在上一个输出中注意到什么令人惊讶的地方吗？翻回几页找找线索....

`zcat`命令本应与`compress`实用程序相关联，但你可以看到它显然是`gzip`压缩命令家族的一部分。

这里发生了什么？

这个谜题的解决方案是`gzip`的一个鲜为人知的特性是，它不仅可以解压缩自己的压缩文件格式，还可以解压缩来自`compress`、`zip`和`pack`的文件！

- 6. 如果你不断遇到磁盘空间问题而买不起更大的磁盘，你可以将`gzip`与`find`结合使用，自动遍历用户文件并自动压缩任何异常大的文件：

```
$ find /home -type f -size +1000k -print
/home/taylor/Gator/Snapshots/MAILOUT.tar.Z
/home/taylor/IBM/fop.jar
/home/taylor/IBM/j2sdk_1_3_0_02-solx86.tar
/home/taylor/Lynx/src/lynx
/home/taylor/Lynx/lynx
/home/taylor/maillog.txt.gz
/home/taylor/Nice Work.mp3.gz
```

这个特定命令列出所有大于`1000Kb`的文件（`-type f`）。

将此转换为完全可用的`shell`脚本需要若干步骤，但这次我们直接跳到最终产品：

```
# cat autocompress.sh
#!/bin/sh

# AUTOCOMPRESS : automatically find and compress excessively large files
# in the /home directory tree, sending email to the user so they know
# what’s happened.

homedir="/home"
threshold="+1000k"  # files must be bigger than this to compress
```
