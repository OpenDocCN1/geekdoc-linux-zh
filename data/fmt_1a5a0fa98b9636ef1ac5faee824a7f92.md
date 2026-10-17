
```bash
# fbackup -f tapesys:/dev/rmt/0m -i /var/tmp -v
fbackup(1004): session begins on Wed Jul 12 15:56:22 2000
fbackup(3507): volume 1 has been used 1 time(s) (maximum: 100)
fbackup(3024): writing vol 1 to output file tapesys:/dev/rmt/0m
1: /
2: /var
3: /var/tmp
4: /var/tmp/AAAA1812 0
5: /var/tmp/AAAA1992 0
6: /var/tmp/BEQ19522 19
7: /var/tmp/DCB19522 0
8: /var/tmp/DBC19522 0
9: /var/tmp/ISPX19522 0
.
.
.
73: /var/tmp/eaaa13306 1
74: /var/tmp/ems_inittab.old 2
75: /var/tmp/envd.action2 1
76: /var/tmp/envd.action5 1
77: /var/tmp/inet.conf.old 9
78: /var/tmp/net19522 1799
79: /var/tmp/swagent.log 16
fbackup(1005): run time: 43 seconds
fbackup(3055): total file blocks read for backup: 1974
fbackup(3056): total blocks written to output file ori:/dev/rmt/0m: 0
#
```

此命令通过系统将文件发送到系统 `tapesys` 上的磁带驱动器，从而在系统 `or1` 上执行 `/var/tmp` 的备份。我们可以使用许多其他选项给 `fbackup`，如前面的示例所示，但我希望保持示例简单，以便容易看出远程磁带驱动器的指定方式。

### dd

`dd` 是一个用于将设备（如磁盘）的内容写入磁带的实用程序。您还可以使用 `dd` 将磁带的映像复制到系统上的文件中，然后查看该文件。

首先，让我们使用 `tar` 将目录的内容写入磁带；然后使用 `dd` 将磁带内容复制为文件。在此示例中，`dd` 唯一需要的选项是 `if`，它指定输入文件为磁带驱动器。

```bash
% cd /var/tmp
# tar cf /dev/rmt/0m ~ `ls`
# cd /tmp
# dd if=/dev/rmt/0m > /tmp/tapecontents
183+0 records in
183+0 records out
# tar tv /tmp/tapecontents
rw-------  0/3      0 Jul 11 15:57 2000 CBAMFEAa01630
rw-------  0/3      0 Jul 11 15:20 2000 CBAMHBAa01020
rw-------  0/3      0 Jul 11 15:50 2000 CBAMHBAa01540
rw-------  0/3    336 Jul 12 13:18 2000 CBAMHBAa07762
rw-------  0/3    102 Jul 12 13:44 2000 CBAMHBAa08333
rw-rw-rw-  0/3    102 Jul 11 15:20 2000 aaaa01112
.
rw-rw-rw-  0/3     28 Jul 11 15:45 2000 esa01487
rwxr-x--  0/0     28 Jul 11 21:53 2000 envd.action2
rwxr-x--  0/0     28 Jul 11 21:53 2000 envd.action5
rw-rw-rw-  0/3    2304 Jul 12 12:42 2000 exclude.temp
r-xr-xr-x  2/2      0 Jul 11 13:50 2000 ntp/
rw-r--r--  0/3    1595 Jul 12 12:23 2000 swagent.log
rw-rw-rw-  0/3     205 Jul 12 12:39 2000 tmp_cfg_file
#
```

现在，我们可以像前面章节所示那样，使用 `tar` 查看文件内容，命令如下：

```bash
# tar tv /tmp/tapecontents
```

`dd` 的另一个常见用途是将远程系统磁带驱动器上的 `cpio` 归档提取到本地系统。在以下示例中，没有磁带驱动器的本地系统是 `orl`，具有磁带驱动器的远程系统是 `tapessys`。我们将使用 `dd` 和 `cpio` 将磁带读取到 `orl` 上的一个目录中（有关选项的解释，请参阅前面的 `cpio` 章节），示例如下：

```bash
# hostname
orl
# pwd
/tmp/remotecpiofiles
# remsh tapessys "dd if=/dev/rmt/0m bs=8k" | cpio -icvBdum
.
envd.action2
envd.action5
swagent.log
ntp
CBAMHBAo01020
aaaa01558
.
.
.
.
aaaa01487
CBAMFEAa01630
cmd_res8215
tmp_cfg_file
cmd_res8708
CBAMHBAb07762
exclude.temp
arch.include.1
3580 blocks
0+358 records in
0+358 records out
#
```

该命令运行远程 shell（`remsh`）以在 `tapessys` 上执行 `dd` 命令。此命令的输出通过管道传输到我们本地系统的 `cpio`，以提取归档。在此示例中，仅使用 `if` 选项来指定输入文件。指定输出文件的 `of` 选项不需要。如果您要对磁盘设备执行 `dd` 操作将其写入磁带驱动器，则 `of` 将是您系统上的磁带驱动器，例如 `/dev/rmt/0m`。

### dump 和 restore

`dump` 类似于 `backup`。如果在 HP-UX 上使用 `backup`，您会发现使用 `dump` 时有很多相似之处。`dump` 作为备份方案的一部分提供级别，并创建 `/var/adm/dumpdates`，该文件列出了文件系统最后备份的时间。`restore` 用于读取使用 `dump` 备份的信息。然而，`dump` 仅适用于 HFS 文件系统，不适用于 VxFS，并且假设您使用的是盒式磁带。`vxdump` 和 `vxrestore` 用于 VxFS。一般来说，您不会看到在 HP-UX 上推荐 `dump`（以及 `vxdump`）和 `restore`（以及 `vxrestore`）作为备份和恢复程序。`fbackup` 和 `cpio` 是 HP-UX 上首选的备份程序。然而，只要您牢记文件系统类型的限制，使用 `dump` 和 `restore` 是没有理由不行的。

让我们看看一些使用 `dump` 和 `restore` 的示例。我们的示例实际上将使用 `vxdump` 和 `vxrestore`；然而，HFS 和 VxFS 程序的使用方式几乎相同。我们将在接下来的示例中使用几条命令，包括以下内容：

```bash
# vxdump 0fu /dev/rmt/0m /var  ; dump vxfs file system /var to tape
# /dev/rmt/0m using level 0 and update /var/adm/dumpdates.

# vxrestore tf /dev/rmt/0m | grep eaaa  ; obtain table of contents from

# vxrestore -x -f /dev/rmt/0m ./tmp/eaaa01487  ; restore file to current directory
```

让我们更详细地查看其中一些命令，我将提供关于正在发生的事情的更多解释。

我们的第一个示例运行 `vxdump`，以备份级别 0（完全备份）备份目录 `/var`，使用 `f` 选项指定输出文件 `/dev/rmt/0m`，并使用 `u` 向 `/var/adm/dumpdates` 写入：
