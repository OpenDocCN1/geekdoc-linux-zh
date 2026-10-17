
```bash
$ stat /etc/hosts
 File: `/etc/hosts'     Blocks: 8           IO Block: 4096 regular file
 Size: 2667            Blocks: 8           IO Block: 4096 regular file
 Device: 805h/2053d    Inode: 788         Links: 1
 Access: (0644/-rw-r--r--)  Uid: (    0/    root)   Gid: (    0/    root)
 Access: 2009-05-25 20:47:14.916626707 -0500
 Modify: 2009-05-25 20:46:57.516293325 -0500
 Change: 2009-05-25 20:46:57.516293325 -0500
```

使用 `stat` 命令显示 `/etc/hosts` 文件的信息

`stat` 命令显示关于文件的扩展信息。它包含使用 `ls` 命令时无法获取的有用信息，例如文件的最后访问时间以及关于文件在文件系统中位置的技术信息。上述示例显示了 `/etc/hosts` 文件的 `stat` 输出。下一个示例显示了 `/etc` 目录本身的 `stat` 输出。

```bash
$ stat /etc
 File: `/etc'
 Size: 4096            Blocks: 8           IO Block: 4096 directory
 Device: 801h/2049d    Inode: 316993      Links: 75
 Access: (0755/drwxr-xr-x)  Uid: (    0/    root)   Gid: (    0/    root)
 Access: 2010-04-01 12:17:44.000000000 -0500
 Modify: 2010-03-28 12:47:21.000000000 -0500
 Change: 2010-03-28 12:47:21.000000000 -0500
```

显示目录的 `stat` 输出

`-f` 选项可用于 `stat` 以显示整个文件系统的相关信息，如下一个示例所示。

```bash
$ stat -f /
 File: "/"
 Id: e70b9c097a45b919   Namelen: 255     Type: ext2/ext3
 Block size: 4096       Fundamental block size: 4096
 Blocks: Total: 9965379  Free: 9723316    Available: 9221085
 Inodes: Total: 2514944  Free: 2476388
```

使用 `-f` 选项与 `stat` 显示关于文件系统的信息

常见用法示例：

| 命令 | 描述 |
| :--- | :--- |
| `stat [FILE/DIR]` | 显示指定文件/目录的信息 |
| `stat -f [FILESYSTEM]` | 显示指定文件系统的相关信息 |

### date

**用途：** 显示或设置系统时钟。

**用法语法：** `date [OPTIONS] [TIME/DATE]`

```bash
$ date
Wed Jun 10 20:33:27 CDT 2009
```

![](img/fa2f95b64a707c963dfa0445bd9281a7_31_0.png)

`date` 命令显示本地系统的当前时间和日期，如上图示例所示。

> **注意**：Unix、Linux 和 BSD 系统以 24 小时制追踪时间。

可以使用 `-s` 选项来设置系统的时间/日期，如下一示例所示。

```bash
$ date -s "07/10/2009 11:30"
Fri Jul 10 11:30:00 CDT 2009
```

![](img/fa2f95b64a707c963dfa0445bd9281a7_31_1.png)

当同时设置时间和日期时，必须使用 `"MM/DD/YYYY HH:MM"` 格式。若仅设置时间，只需使用 `date -s HH:MM`。

> **注意**：必须登录为 `root` 或使用 `sudo` 命令（见第 91 页讨论内容）才能设置系统时钟。

**常用用法示例：**

| 命令 | 描述 |
| :--- | :--- |
| `date` | 显示时间和日期 |
| `date -s [HH:MM]` | 设置时间 |
| `date -s ["MM/DD/YYYY HH:MM"]` | 设置时间和日期 |

### cal

**用途：** 在命令行上显示日历。

**用法语法：** `cal [OPTIONS] [MONTH] [YEAR]`

```bash
$ cal
      May 2009
Su Mo Tu We Th Fr Sa
                  1
 2          3          4          5          6          7          8
 9         10         11         12         13         14         15
16         17         18         19         20         21         22
23         24         25         26         27         28         29
30
31
```

![](img/fa2f95b64a707c963dfa0445bd9281a7_32_0.png)

`cal` 命令在命令行上显示一个简单的日历。不带参数执行 `cal` 将显示当前月份的日历，如上图示例所示。添加月份和年份作为参数将显示指定月份和年份的日历，如下一示例所示。

```bash
$ cal 8 2009
      August 2009
Su Mo Tu We Th Fr Sa
                  1
 2          3          4          5          6          7          8
 9         10         11         12         13         14
15
16         17         18         19         20         21
22
23         24         25         26         27         28         29
30
```

![](img/fa2f95b64a707c963dfa0445bd9281a7_32_1.png)

**常用用法示例：**

| 命令 | 描述 |
| :--- | :--- |
| `cal` | 显示当前月份的日历 |
| `cal -m` | 显示周一为一周的第一天 |
| `cal [MONTH] [YEAR]` | 显示指定月份和年份的日历 |
| `cal [YEAR]` | 显示指定年份的日历 |
| `cal -y` | 显示当前年份的日历 |

### history

**用途：** 显示最近执行的命令。

**用法语法：** `history [OPTIONS]`

```bash
$ history 10
 686  man uptime
 687  cat /etc/hosts
 688  ls -l
 689  uptime
 690  dmesg
 691  iostat
 692  vmstat
 693  ping google.com
 694  tracepath google.com
 695  history 10
```

![](img/fa2f95b64a707c963dfa0445bd9281a7_33_0.png)

`history` 命令显示用户的命令行历史记录。不带参数执行 `history` 命令将显示当前用户的完整命令行历史记录。若需较短的列表，可以指定一个数字作为参数。例如，输入 `history 10` 将显示当前用户最近执行的 10 条命令，如上图示例所示。

> **提示**：您可以使用 `! [NUM]` 来执行之前的命令，其中 `NUM` 是您在历史记录中想要调用的行号。例如，执行 `!687` 将重新运行上例中第 687 行列出的命令。

在 Linux 中，每个用户的主目录中都有一个名为 `.bash_history` 的文件，其中包含其命令行历史记录。Unix 系统通常将历史记录存储在名为 `.sh_history` 或 `.history` 的文件中。
