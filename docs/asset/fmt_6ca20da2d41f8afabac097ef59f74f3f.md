
## 7.4. 简单备份

如果你想每天进行备份并有六卷磁带，你可以使用磁带 1 进行第一次全备份（例如，在周五），并使用磁带 2-5 卷进行增量备份（周一至周四）。然后在磁带 6 上进行新的全备份（第二个周五），然后再次开始使用 2-5 卷磁带进行增量备份。在获得新的全备份之前，你不想用磁带 1 覆盖，以防在制作全备份期间发生故障。当你完成磁带 6 的全备份后，你想将磁带保存在其他地方，这样即使你的其他备份磁带在火灾中损坏，你至少还会留有一些东西。当你需要进行下次全备份时，用磁带 1 代替磁带 6。

如果你超过六卷磁带，可以使用额外的磁带进行全备份。每次进行全备份时，使用最旧的一卷磁带。这样你就可以拥有过去几周的全备份，如果你想寻找旧的已删除文件或文件的旧版本，这将很有。

### 7.4.1 使用 tar 进行备份

可以使用 `tar` 轻松制作全备份：

```
# tar --create --file /dev/ftape /usr/src
tar: Removing leading / from absolute path names in the archive
#
```

上面的示例使用了 GNU 版本的 `tar` 及其长选项名称。传统的 `tar` 版本只识别单个字符。GNU 版本还可以处理无法放入单卷磁带或软磁盘的备份，或者路径非常路径的备份；并非所有版本的 `tar` 都能做这些事情（Linux 仅使用 GNU `tar`）。

如果你的备份无法放入单卷磁带，则需要使用 `--multi-volume (-M)` 选项：

```
# tar -CMf /dev/fd0H140 /usr/src
tar: Removing leading / from absolute path names in the archive
Prepare volume #2 /dev/fd0H140 and hit return:
#
```

注意，你应该在开始备份之前格式化软磁盘，或者使用另一个窗口或虚拟终端，在 `tar` 请求新磁带时进行操作。

完成备份后，你应该使用 `--compare (-d)` 选项检查备份是否正常：

```
# tar --compare --verbose /dev/ftape
usr/src/
usr/src/linux
usr/src/linux-1.2.10-includes/
#
```

不检查备份意味着在你丢失原始数据之前，你不会注意到备份是否正常工作。

可以使用 `tar` 配合 `--newer (-N)` 选项进行增量备份：

```
# tar --create --newer '8 Sep 1995' --file /dev/ftape /usr/src
--verbose
tar: Removing leading / from absolute path names in the archive
usr/src/
usr/src/linux
usr/src/linux-1.2.10-includes/
usr/src/linux-1.2.10-includes/include/
usr/src/linux-1.2.10-include/linux/modules/
usr/src/linux-1.2.10-include/asm-generic/
usr/src/linux-1.2.10-include/asm-1386/
usr/src/linux-1.2.10-include/asm-mips/
usr/src/linux-1.2.10-include/asm-alpha/
usr/src/linux-1.2.10-includes/include/asm-m68/
usr/src/linux-1.2.10-includes/include/asm-sparc/
usr/src/patch-1.2.11.gz
```

遗憾的是，`tar` 无法注意到文件的 inode 信息何时发生了变化，例如其权限位被更改，或者其名称被更改。可以使用 `find` 并比较当前文件系统状态与已备份的文件列表来解决此问题。执行此操作的脚本和程序可以在 Linux ftp 站点上找到。

### 7.4.2 使用 tar 恢复文件

`tar` 的 `--extract (-x)` 选项提取文件：

```
# tar extract --same-permissions --verbose --file /dev/fd0H1440
usr/src/
usr/src/linux
usr/src/linux-1.2.10-includes/
usr/src/linux-1.2.10-includes/include/
usr/src/linux-1.2.10-includes/include/linux/
usr/src/linux-1.2.10-includes/include/hdreg.h
usr/src/linux-1.2.10-includes/include/kernel.h
#
```

你也可以通过在命令行中指定名称来提取特定的文件或目录（包括所有文件和子目录）：

```
# tar xpv /dev/fd0H1440 usr/src/linux-1.2.10-includes/include/linux/hdreg.h
usr/src/linux-1.2.10-includes/include/linux/hdreg.h
#
```

如果你想查看备份卷上存哪些文件，请使用 `--list (-t)` 选项：

```
# tar --list --file /dev/fd0H1440
usr/src/
usr/src/linux
usr/src/linux-1.2.10-includes/
usr/src/linux-1.2.10-includes/include/
```

# 图 7.1 一个多级备份计划示例。

| 1 | 3 | 4 | 5 | 6 | 2 | 3 | 4 | 5 | |

|---|---|---|---|---|---|---|---|---|---|

| 022221 | 022221 | 022221 | 022221 | 022220 | 022221 | 022221 | 022221 | 022221 | |

| | | | | | | | | | 磁带编号 |

| 1 | 8 | 15 | 22 | 29 | 31 | 8 | 15 | 22 | 29 31 日 |

| 周一 | 周一 | 周一 | 周一 | 周一 | 周一 | 周一 | | 备份级别 |

# 使用多个备份级别的高效备份方案

| 磁带 | 级别 | 备份（天） | 恢复磁带 |
|---|---|---|---|
| 1 | 0 | n/a | 1 |
| 2 | 3 | 1 | 1, 2 |
| 3 | 2 | 2 | 1, 3 |
| 4 | 5 | 1 | 1, 2, 4 |
| 5 | 4 | 2 | 1, 2, 5 |
| 6 | 7 | 1 | 1, 2, 5, 6 |
| 7 | 6 | 2 | 1, 2, 5, 7 |
| 8 | 9 | 1 | 1, 2, 5, 7, 8 |
| 9 | 8 | 2 | 1, 2, 5, 7, 9 |
| 10 | 9 | 1 | 1, 2, 5, 7, 9, 10 |
