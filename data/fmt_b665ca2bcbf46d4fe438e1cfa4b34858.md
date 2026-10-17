
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

`vxdump` 会将与备份相关的信息输出到标准输出。

接下来，让我们使用 `vxrestore` 查看磁带上的目录，查找以 `eaaa` 开头的文件。然后，我们将从系统中删除这些文件中的一个，并使用 `vxrestore` 从磁带中恢复它。要生成目录，我们使用 `t` 选项；要从磁带中提取文件，我们使用 `vxrestore` 的 `x` 选项，如下列清单所示：

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

本节的示例展示了使用 `vxdump` 创建备份磁带、生成目录以及使用 `vxrestore` 进行恢复。虽然 `fbackup` 和 `cpio` 是 HP-UX 上推荐的备份解决方案，但如果您熟悉这些程序并希望使用它们，可以使用 `dump` 和 `restore`。由于 `tar` 的可移植性，它也经常被用于备份和恢复。

## 第 8 章

### 系统启动和关闭脚本

## 虚拟分区中的系统启动和关闭脚本

每个虚拟分区都有独立的启动和关闭脚本，就像在独立系统上一样。由于虚拟分区，在启动和关闭方面没有独特的活动；但是，由于每个 vPar 都在运行自己的 HP-UX，您可以定制启动和关闭以满足您在每个 vPar 中运行的应用程序的需求。此外，还有一个 `heartbeat` 守护进程，用于每隔几秒同步一次虚拟分区数据库。

让我们看看在 vPar 中运行的应用程序以及支持该应用程序所使用的启动和关闭过程。此外，我们还将查看启动和停止 `heartbeat` 守护进程以同步虚拟分区数据库的方式。

### 虚拟分区中的应用启动

每个虚拟分区就像一台独立的服务器。在 vPar 中运行的应用程序独立于其他 vPar 中运行的应用程序和活动。

vPar 中的所有应用程序都需要运行启动脚本，就像在任何系统上一样（如果您需要了解 HP-UX 启动和关闭如何工作，请参阅本章中非 vPar 特定的部分）。

在本示例中使用的 vPar 中，我们运行了多种应用程序，包括 BroadVision。让我们查看 `etc/rc.config.d`，配置变量脚本位于此处，看看存在哪些 `bv` 文件（与 BroadVision 相关的文件）：

```bash
# ll | grep bv
-rwxr-xr-x    1 root        sys          9 Sep 26 09:31 bv
# cat bv
BV_CTL=1
#
```

此清单显示了 `bv` 文件及其内容。`BV_CTL=1` 变量表示当系统启动时应启动 BroadVision。

启动 `bv` 应用程序进程会导致启动多个与 BroadVision 相关的守护进程，包括以下清单中所示的那些：

```bash
# ps -ef | grep bv1
pbcosmb    3111    3096   0 Sep 26 ?        0:04 bvcont_srv_p_1221_3 -f -install_name bv1tol/bvcont_srv...
pbcosv    3404    3096   0 Sep 26 7        1:19 cntcdb_p_1221_5 -install_name bv1tol/cntcdb_1
pbcosbv   3707    3096   0 Sep 26 7        0:20 genericdb_p_1221_6 -install_name bv1tol/genericdb_1
pbcosbv   3479    3096   0 Sep 26 7:05 cntdb_p_1221_7 -install_name bv1tol DiscussionForus_cntdb_1
root        7572    7232   0 13:17:33 pts/0                0:00 grep bv1
#
```

您可以看到，此系统上正在运行许多与 `bv1` 应用程序相关的进程。这些进程作为 HP-UX 启动结构的一部分自动启动。以下清单显示了运行级别一（`/sbin/rc1.d`）和运行级别二（`/sbin/rc2.d`）中 `bv` 的链接。

```bash
# ll /sbin/rc1.d | grep bv
lrwxr-xr-x    1 root        sys          15 Sep 26 10:42 F10sbv -> /sbin/init.d/bv
# ll /sbin/rc2.d | grep bv
lrwxr-xr-x    1 root        sys          15 Sep 26 10:41 S930bv -> /sbin/init.d/bv
#
```

### 虚拟分区中的应用启动

如链接前的 `K` 所示，`bv_kill` 脚本显示在 `/sbin/rc1.d` 中；如链接前的 `S` 所示，`start` 脚本显示在 `/sbin/rc2.d` 中。

在链接中显示的脚本 `/sbin/init.d/bv` 会在虚拟分区的启动和关闭时运行各种命令。以下清单展示了 `/sbin/init.d/bv` 脚本：
