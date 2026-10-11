
```
# hostname
or1
# pwd
/tmp/remotecpiofiles
# remsh tapesys "dd if=/dev/rmt/0m bs=8k" | cpio -icvdum

envd.action2
envd.action5
swagent.log
ntp
OBAMHBAa01020
aaa01558

eaaa01487
OBAMFEAa01630
cmd_res8215
tmp_cfg_file
cmd_res8708
OBAMHBAa07762
exclude.temp
arch.include.1
3580 blocks
0+358 records in
0+358 records out
#
```

![](img/6969df54e516231f8e64fd1177ac1127_353_2.png)

该命令运行远程 shell (`remsh`) 在 `tapesys` 上运行 `dd` 命令。该命令的输出通过到本地系统的 `cpio` 以提取存档。在此示例中，仅使用了 `if` 选项来指定输入文件。不需要指定输出文件的 `of` 选项。如果你对设备到磁带驱动器执行 `dd`，`of` 将是你系统上的磁带驱动器，例如 `/dev/rmt/0m`。

# dump 和 restore

`dump` 与 `fbackup` 相似。如果你在 HP-UX 上使用 `fbackup`，当你使用 `dump` 时会发现许多相似之处。`dump` 作为备份方案的一部分提供了级别并创建 `/var/adm/dumpdates`，列出文件系统最后备份的时间。`restore` 用于读取用 `dump` 备份的信息。然而，`dump` 适用于 HFS 文件系统，不适用于 VxFS，并且它假设你使用的是卷带，`vxdump` 和 `vxrestore` 用于 VxFS。通常情况下，你不会在 HP-UX 上找到 `dump`（以及 `vxdump`）和 `restore`（以及 `vxrestore`）作为备份和恢复程序的推荐，`fbackup` 和

## 第 6 章 备份

```
# fbackup -f tapesys:/dev/rmt/0m -i /var/tmp -v
fbackup(1004): session begins on Wed Jul 12 14:56:22 2000
fbackup(3307): volume 1 has been used -1 time(s) (maximum: 100)
fbackup(3024): writing vol 1 to output file tapesys:/dev/rmt/0m
1: / 2
2: /var 2
3: /var/tmp 4
4: /var/tmp/AAA11812 0
5: /var/tmp/AAAa1992 0
6: /var/tmp/BEQ19522 19
7: /var/tmp/DCE19522 0
8: /var/tmp/DEC19522 0
9: /var/tmp/ISPX19522 0
.
.
73: /var/tmp/eaa13306 1
74: /var/tmp/ems_inittab.old 2
75: /var/tmp/envd.action2 1
76: /var/tmp/envd.action5 1
77: /var/tmp/inetd.conf.old 9
78: /var/tmp/net19522 1799
79: /var/tmp/swagent.log 16
fbackup(1005): run time: 43 seconds
fbackup(3055): total file blocks read for backup: 1974
fbackup(3056): total blocks written to output file orl:/dev/rmt/0m: 0
#
```

该命令通过将文件发送到系统 `tapesys` 磁带驱动器，对系统 `orl` `/var/tmp` 进行备份。我们可以像之前的示例演示的那样为 `fbackup` 使用许多额外的选项，但我想保持示例简单，以便于查看远程驱动器的指定。

![](img/6969df54e516231f8e64fd1177ac1127_351_0.png)

# dd

`dd` 是一个将设备（如磁盘）的内容写入磁带的实用。你也可以使用 `dd` 将磁带镜像拷贝到系统上的文件，然后就可以查看该文件。首先，让我们使用 `tar` 将目录的内容写入磁带，然后使用 `dd` 将磁带拷贝为文件。此示例中 `dd` 唯一需要的选项是 `if`，它指定磁带为输入文件。

```
# cd /var/tmp
# tar cf /dev/rmt/0m
# cd /tmp
# dd if=/dev/rmt/0m > /tmp/tapecontents
183+0 records in
183+0 records out
# tar tv /tmp/tapecontents
rw------- 0/3 Jul 11 15:57 2000 OAMHBAAa01630
rw------- 0/3 Jul 11 15:20 2000 OAMHBAAa01020
rw------- 0/3 Jul 11 15:50 2000 OAMHBAAa01540
rw------- 0/3 336 Jul 12 13:18 2000 OAMHBAAa07762
rw------- 0/3 Jul 12 12:44 2000 OAMHBAAa0833
rw-rw-rw- 0/3 Jul 11 15:20 2000 aaaa01112
```

```
rw-rw-rw- 0/3 Jul 28 15:45 2000 eaaa01487
xr-xr-xr- 0/0 Jul 28 21:53 2000 envd.action2
xr-xr-xr- 0/0 Jul 28 21:53 2000 envd.action5
rw-rw-rw- 0/3 2304 Jul 12 12:42 2000 exclude.temp
xr-xr-xr- 2/2 0 Jul 11 13:50 2000 ntp/
rw-rw-rw- 0/3 1595 Jul 12 12:23 2000 swagent.log
rw-rw-rw- 0/3 205 Jul 12 12:39 2000 tmp_cfg_file
#
```

现在我们可以使用 `tar` 正如之前的章节所示，查看文件内容：

### `tar tv /tmp/tapecontents`

`dd` 的另一个常见用法是从远程系统的磁带驱动器提取 `cpio` 存档到本地系统。在下面的示例中，没有磁带的本地系统是 `or1`，带磁带的远程系统是 `tapesys`。我们将使用 `dd` 和 `cpio` 将磁带读取到 `or1` 上的目录（关于后续示例中选项的解释，请参见之前的 `cpio` 章节）：

![](img/6969df54e516231f8e64fd1177ac1127_353_0.png)

![](img/6969df54e516231f8e64fd1177ac1127_353_1.png)

```
# hostname
or1
# pwd
/tmp/remotecpiofiles
# remsh tapesys "dd if=/dev/rmt/0m bs=8k" | cpio -icvdum

envd.action2
envd.action5
swagent.log
ntp
OBAMHBAa01020
aaa01558

eaaa01487
OBAMFEAa01630
cmd_res8215
tmp_cfg_file
cmd_res8708
OBAMHBAa07762
exclude.temp
arch.include.1
3580 blocks
0+358 records in
0+358 records out
#
```

![](img/6969df54e516231f8e64fd1177ac1127_353_2.png)

该命令运行远程 shell (`remsh`) 在 `tapesys` 上运行 `dd` 命令。该命令的输出通过到本地系统的 `cpio` 以提取存档。在此示例中，仅使用了 `if` 选项来指定输入文件。不需要指定输出文件的 `of` 选项。如果你对设备到磁带驱动器执行 `dd`，`of` 将是你系统上的磁带驱动器，例如 `/dev/rmt/0m`。

# dump 和 restore
