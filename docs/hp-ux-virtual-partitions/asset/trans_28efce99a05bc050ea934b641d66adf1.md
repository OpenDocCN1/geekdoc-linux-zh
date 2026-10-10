
# dd

**dd** 是一个用于将设备（如磁盘）的内容写入磁带的实用程序。您还可以使用 **dd** 将磁带的映像复制到系统上的文件中，然后查看该文件。

首先，让我们使用 **tar** 将目录的内容写入磁带；然后使用 **dd** 将磁带内容复制为文件。在此示例中，**dd** 唯一需要的选项是 *if*，它指定输入文件为磁带驱动器。

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

现在，我们可以像前面章节所示那样，使用 **tar** 查看文件内容，命令如下：

```bash
# tar tv /tmp/tapecontents
```

**dd** 的另一个常见用途是将远程系统磁带驱动器上的 **cpio** 归档提取到本地系统。在以下示例中，没有磁带驱动器的本地系统是 *orl*，具有磁带驱动器的远程系统是 *tapessys*。我们将使用 **dd** 和 **cpio** 将磁带读取到 *orl* 上的一个目录中（有关选项的解释，请参阅前面的 **cpio** 章节），示例如下：

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

该命令运行远程 shell（**remsh**）以在 *tapessys* 上执行 **dd** 命令。此命令的输出通过管道传输到我们本地系统的 **cpio**，以提取归档。在此示例中，仅使用 *if* 选项来指定输入文件。指定输出文件的 *of* 选项不需要。如果您要对磁盘设备执行 **dd** 操作将其写入磁带驱动器，则 *of* 将是您系统上的磁带驱动器，例如 */dev/rmt/0m*。

## dump 和 restore

**dump** 类似于 **backup**。如果在 HP-UX 上使用 **backup**，您会发现使用 **dump** 时有很多相似之处。**dump** 作为备份方案的一部分提供级别，并创建 **/var/adm/dumpdates**，该文件列出了文件系统最后备份的时间。**restore** 用于读取使用 **dump** 备份的信息。然而，**dump** 仅适用于 HFS 文件系统，不适用于 VxFS，并且假设您使用的是盒式磁带。**vxdump** 和 **vxrestore** 用于 VxFS。一般来说，您不会看到在 HP-UX 上推荐 **dump**（以及 **vxdump**）和 **restore**（以及 **vxrestore**）作为备份和恢复程序。**fbackup** 和 **cpio** 是 HP-UX 上首选的备份程序。然而，只要您牢记文件系统类型的限制，使用 **dump** 和 **restore** 是没有理由不行的。

让我们看看一些使用 **dump** 和 **restore** 的示例。我们的示例实际上将使用 **vxdump** 和 **vxrestore**；然而，HFS 和 VxFS 程序的使用方式几乎相同。我们将在接下来的示例中使用几条命令，包括以下内容：

```bash
# vxdump 0fu /dev/rmt/0m /var  ; dump vxfs file system /var to tape
# /dev/rmt/0m using level 0 and update /var/adm/dumpdates.

# vxrestore tf /dev/rmt/0m | grep eaaa  ; obtain table of contents from

# vxrestore -x -f /dev/rmt/0m ./tmp/eaaa01487  ; restore file to current directory
```

让我们更详细地查看其中一些命令，我将提供关于正在发生的事情的更多解释。

我们的第一个示例运行 **vxdump**，以备份级别 0（完全备份）备份目录 **/var**，使用 *f* 选项指定输出文件 **/dev/rmt/0m**，并使用 *u* 向 **/var/adm/dumpdates** 写入：

```bash
# vxdump 0fu /dev/rmt/0m /var

vxdump: Date of this level 0 dump: Tue Jul 11 16:41:27 2000
vxdump: Date of last level 0 dump: the epoch
vxdump: dumping /dev/vg00/rvol10 to /dev/rmt/0m
vxdump: mapping (Pass I) [regular files]
vxdump: mapping (Pass II) [directories]
vxdump: estimated 428058 blocks (209.01MB).
vxdump: dumping (Pass III) [directories]
vxdump: dumping (Pass IV) [regular files]
vxdump: 214146 tape blocks on 1 volumes(s)
vxdump: level 0 dump on Tue Jul 11 16:41:27 2000
vxdump: closing /dev/rmt/0m
vxdump: vxdump is done
#
```

**vxdump** 会将与备份相关的信息输出到标准输出。

接下来，让我们使用 **vxrestore** 查看磁带上的目录，查找以 *eaaa* 开头的文件。然后，我们将从系统中删除这些文件中的一个，并使用 **vxrestore** 从磁带中恢复它。要生成目录，我们使用 *t* 选项；要从磁带中提取文件，我们使用 **vxrestore** 的 *x* 选项，如下列清单所示：

```bash
# vxrestore tf /dev/rmt/0m | grep eaaa
404 ../tmp/eaaa01299
678 ../tmp/eaaa01333
700 ../tmp/eaaa01354
736 ../tmp/eaaa01380
741 ../tmp/eaaa01405
717 ../tmp/eaaa01487

#
#
# rm /var/tmp/eaaa01487
#
# vxrestore -x -f /dev/rmt/0m ./tmp/eaaa01487
# You have not read any tapes yet.
# Unless you know which volume your file(s) are on you should start
# with the next volume and work towards the first.
# Specify next volume #: 1
# set owner/mode for '..' [yn] y

# cd /var/tmp
# ls -1 eaaa01487
total 2
-rw-rw-rw- 1 root sys 28 Jul 11 15:45 eaaa01487
#
```

请注意，在恢复文件的过程中，我们必须指定卷号 1 以及是否要设置文件的模式。

本节的示例展示了使用 **vxdump** 创建备份磁带、生成目录以及使用 **vxrestore** 进行恢复。虽然 **fbackup** 和 **cpio** 是 HP-UX 上推荐的备份解决方案，但如果您熟悉这些程序并希望使用它们，可以使用 **dump** 和 **restore**。由于 **tar** 的可移植性，它也经常被用于备份和恢复。

## 第 8 章

## 系统启动和关闭脚本

### 虚拟分区中的系统启动和关闭脚本

每个虚拟分区都有独立的启动和关闭脚本，就像在独立系统上一样。由于虚拟分区，在启动和关闭方面没有独特的活动；但是，由于每个 vPar 都在运行自己的 HP-UX，您可以定制启动和关闭以满足您在每个 vPar 中运行的应用程序的需求。此外，还有一个 *heartbeat* 守护进程，用于每隔几秒同步一次虚拟分区数据库。

让我们看看在 vPar 中运行的应用程序以及支持该应用程序所使用的启动和关闭过程。此外，我们还将查看启动和停止 *heartbeat* 守护进程以同步虚拟分区数据库的方式。

### 虚拟分区中的应用启动

每个虚拟分区就像一台独立的服务器。在 vPar 中运行的应用程序独立于其他 vPar 中运行的应用程序和活动。

vPar 中的所有应用程序都需要运行启动脚本，就像在任何系统上一样（如果您需要了解 HP-UX 启动和关闭如何工作，请参阅本章中非 vPar 特定的部分）。

在本示例中使用的 vPar 中，我们运行了多种应用程序，包括 Broadvision。让我们查看 *etc/rc.config.d*，配置变量脚本位于此处，看看存在哪些 *bv* 文件（与 Broadvision 相关的文件）：

```bash
# ll | grep bv
-rwxr-xr-x    1 root        sys          9 Sep 26 09:31 bv
# cat bv
BV_CTL=1
#
```

此清单显示了 *bv* 文件及其内容。*BV_CTL=1* 变量表示当系统启动时应启动 Broadvision。

启动 *bv* 应用程序进程会导致启动多个与 Broadvision 相关的守护进程，包括以下清单中所示的那些：

```bash
# ps -ef | grep bv1
pbcosmb    3111    3096   0 Sep 26 ?        0:04 bvcont_srv_p_1221_3 -f -install_name bv1tol/bvcont_srv...
pbcosv    3404    3096   0 Sep 26 7        1:19 cntcdb_p_1221_5 -install_name bv1tol/cntcdb_1
pbcosbv   3707    3096   0 Sep 26 7        0:20 genericdb_p_1221_6 -install_name bv1tol/genericdb_1
pbcosbv   3479    3096   0 Sep 26 7:05 cntdb_p_1221_7 -install_name bv1tol DiscussionForus_cntdb_1
root        7572    7232   0 13:17:33 pts/0                0:00 grep bv1
#
```

您可以看到，此系统上正在运行许多与 *bv1* 应用程序相关的进程。这些进程作为 HP-UX 启动结构的一部分自动启动。以下清单显示了运行级别一（*/sbin/rc1.d*）和运行级别二（*/sbin/rc2.d*）中 *bv* 的链接。

```bash
# ll /sbin/rc1.d | grep bv
lrwxr-xr-x    1 root        sys          15 Sep 26 10:42 F10sbv -> /sbin/init.d/bv
# ll /sbin/rc2.d | grep bv
lrwxr-xr-x    1 root        sys          15 Sep 26 10:41 S930bv -> /sbin/init.d/bv
#
```

