
# 10.4 使用 `tar` 进行备份和恢复

## 10.4.1 使用 `tar` 进行备份

可以使用 `tar` 轻松地进行全量备份：

```
# tar -create -file /dev/ftape /usr/src
tar: Removing leading / from absolute path names in the archive
```

上面的示例使用了 GNU 版本的 `tar` 及其长选项名称。传统的 `tar` 版本仅理解单字符选项。GNU 版本还可以处理无法放入单卷磁带或软磁盘的备份，以及处理非常长的路径；并非所有的传统版本都能做到这些。（Linux 仅使用 GNU `tar`。）

如果你的备份无法放入一卷磁带中，你需要使用 `-multi-volume (-M)` 选项：

```
# tar -cmF /dev/fd0H1440 /usr/src

tar: Removing leading / from absolute path names in the archive

Prepare volume #2 for /dev/fd0H1440 and hit return:

#
```

注意，在开始备份之前你应该格式化软磁盘，否则使用另一个窗口或虚拟终端，在 `tar` 询问新软磁盘时进行操作。

完成备份后，你应该使用 `-compare` 选项检查备份是否正常：

```
# tar -compare -verbose -f /dev/ftape

usr/src/

usr/src/linux

usr/src/linux-1.2.10-includes/

#
```

不检查备份意味着直到你丢失原始数据之后，才会发现你的备份没有工作。

可以使用 `tar` 的 `-newer (-N)` 选项进行增量备份：

```
# tar -create -newer '8 Sep 1995' -file /dev/ftape /usr/src -verbose
tar: Removing leading / from absolute path names in the archive
usr/src/
usr/src/linux-1.2.10-includes/
usr/src/linux-1.2.10-includes/include/
usr/src/linux-1.2.10-includes/include/linux/
usr/src/linux-1.2.10-includes/include/modules/
usr/src/linux-1.2.10-includes/include/asm-generic/
usr/src/linux-1.2.10-includes/include/asm-i386/
usr/src/linux-1.2.10-includes/include/asm-mips/
usr/src/linux-1.2.10-includes/include/asm-alpha/
usr/src/linux-1.2.10-includes/include/asm-m68k/
usr/src/linux-1.2.10-includes/include/asm-sparc/
usr/src/patch-1.2.11.gz
#
```

遗憾的是，`tar` 无法察觉文件的节点信息（node）是否发生了变化，例如权限位已更改，或者名称已更改。可以使用 `find` 并将当前文件系统状态与之前备份的文件列表进行比较来解决。执行此操作的脚本和程序可以在 Linux ftp 站点找到。

## 10.4.2 使用 `tar` 恢复文件

`tar` 的 `-extract (-x)` 选项用于提取文件：

```
# tar -extract -same-permissions -verbose -file /dev/ftape
usr/src/
usr/src/linux
usr/src/linux-1.2.10-includes/
usr/src/linux-1.2.10-includes/include/
usr/src/linux-1.2.10-includes/
...
```

全量备份通常比增量备份更费力，因为要写入磁带的数据更多。

恢复过程可以优化，使得你总是备份上次全量备份的所有内容；这样虽然备份会多花一点精力，但永远不需要恢复比一个全量和一个增量备份更多的内容。

如果你想每天进行备份并有六卷磁带，你可以使用磁带 1 进行第一次全量备份（例如在周五），使用磁带 2 到 5 进行增量备份（周一至周四）。然后你在磁带 6 上进行新的全量备份（第二个周五），并再次从磁带 2-5 开始增量备份。在获得新的全量备份之前，你不想覆盖磁带 1，以防在制作全量备份期间发生意外。在你完成到磁带 6 的全量备份后，你希望将磁带 1 保放在其他地方，这样当你的其他备份磁带在文件中损坏时，你至少还有留存。当你需要进行下一次全量备份时，取出磁带 1 并将磁带 6 留在原处。

如果你超过六卷磁带，可以使用额外的磁带进行全量备份。每次备份时，你都使用最旧的那卷磁带。这样你就可以拥有几周以前的全量备份，如果你想找到一个已删除的文件或文件的旧版本，这将很有。
