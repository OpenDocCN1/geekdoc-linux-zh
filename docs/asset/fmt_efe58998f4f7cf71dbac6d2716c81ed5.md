
`/etc/sysconfigtab` -> `..cluster/members/(memb)/boot_partition/etc/sysconfigtab`

记住 `..local..` 是一个指向 `/cluster/members/{memb}` 的 CDSL。在第 6.3 节中，介绍了独立系统上的 CDSL。表 12-1 显示了这些 CDSL：

| `/etc/clu_alias.config` -> `..cluster/members/(memb)/etc/clu_alias.config` |
| `/etc/ntp.drift` -> `..cluster/members/(memb)/etc/ntp.drift` |
| `/etc/ddr.db` -> `..cluster/members/(memb)/boot_partition/etc/ddr.db` |
| `/etc/ddr_base` -> `..cluster/members/(memb)/boot_partition/etc/ddr_base` |
| `/etc/dec_devsw` -> `..cluster/members/(memb)/boot_partition/etc/dec_devsw` |
| `/etc/dec_devsw_bak` -> `..cluster/members/(memb)/boot_partition/etc/dec_devsw_bak` |
| `/etc/dec_hw_ldbc` -> `..cluster/members/(memb)/boot_partition/etc/dec_hw_ldbc` |
| `/etc/fdevdb` -> `..cluster/members/(memb)/boot_partition/etc/fdevdb` |
| `/etc/gen_databases` -> `..cluster/members/(memb)/boot_partition/etc/gen_databases` |
| `/etc/sysconfigtab` -> `..cluster/members/(memb)/boot_partition/etc/sysconfigtab` |

*(注：由于原文表格内容在输入中存在截断或格式偏差，此处根据逻辑进行了对齐翻译处理，保持格式一致)*

```
# rm vmunix vmunix.MOLARI vmunix.sys
```

## 12.2.2 修复损坏的 CDSL

如果你不小心（或或其他原因）删除了 CDSL，可以使用 `mkcdsl(8)` 命令对其进行修复。

例如，我们由于习惯，无意中将一个新内核移动到了根目录。

```
# mv /sys/MOLARI/vmunix /
```

内核现在位于根目录，且 `vmunix` 不再是一个 CDSL。

```
# file vmunix
/vmunix COFF format alpha executable or object module not stripped - version 3.13-14
```

我们知道 `/vmunix` 应该是一个 CDSL，但万一我们不知道了呢？嗯，我们可以运行 `cdslinvchk(8)` 命令，它应该告诉我们缺少哪个链接以及该链接应该是什么。还需要注意的是，`glu_check_config(8)` 也会执行 `cdslinvchk`。

```
# cdslinvchk
Failed CDSL inventory check. See details in /var/adm/cdsl_check_list
```

```
# cat /var/adm/cdsl_check_list
Expected CDSL: ..vmunix -> cluster/members(memb)/boot_partition/vmunix

An administrator or application has replaced this CDSL with:

-rwr-xr-x 1 root system 21009120 Dec 17 12:00 ..vmunix
```

现在我们知道链接应该是什么了，可以使用 `mkcdsl` 命令来修复它。我们将使用 "-b" 选项创建 CDSL，使其指向 `boot_partition`，并使用 "-c" 选项将文件复制到 CDSL 指向的位置。

```
# mkcdsl -bc /vmunix
```

验证操作是否成功。

```
# cdslinvchk
Successful CDSL inventory check.
```

有关 CDSL 以及 `cdslinvchk` 和 `mkcdsl` 命令的更多信息，请参阅第 6 章和或 `cdslinvchk(8)` 和 `mkcdsl(8)` 参考页。

## 12.3 硬件管理回顾

在集群中，硬件管理在很大程度上与独立系统相同，但话回来，Tru64 UNIX 中处理硬件的方式（从 5.0 版本开始）经过重新设计，专门为了适应两点：

- 通到存储设备的多路径。
- TruCluster 服务器。

然而，发生了一些变化，我们认为让你了解这些差异是一个好主意。

### 12.3.1 回顾硬件管理数据库

第一次微小变化发生在创建集群时，之前位于 `/etc` 目录下的某些硬件数据库被移动到每个成员的启动分区，并被替换为 CDLS（图 12-2）。

表 12-2 列出了数据库及其相对于集群或独立系统的位置。

### 12.3.2 回顾 hwmgr (8) 命令

`hwmgr` 命令是集群级的。然而，它必须针对集群才能查看整个集群范围的结果，否则你只能看到特定成员的。。例如，如果你想查看集群上的设备，将使用 "`hwmgr -view device`" 命令。

```
# hwmgr view device | tee hwmgr_view_device.sheridan
| HWID: Device Name | Mfg | Model | Location |
|---|---|---|---|---|
| 3: /dev/dmapi/dmapi | COMPAQ | BD009635C3 | bus-3-targ-0-lun-0 |
| 50: /dev/disk/dsk1c | COMPAQ | BD009635C3 | bus-3-targ-1-lun-0 |
| 52: /dev/disk/dsk2c | COMPAQ | BD009635C3 | bus-3-targ-2-lun-0 |
| 53: /dev/disk/dsk3c | COMPAQ | BD009635C3 | bus-3-targ-3-lun-0 |
| 54: /dev/disk/dsk4c | COMPAQ | BD009635C3 | bus-3-targ-4-lun-0 |
| 55: /dev/disk/dsk6c | COMPAQ | BD009635C3 | bus-3-targ-5-lun-0 |
| 58: scp | | | (unknown) |
| 59: /dev/disk/kevm | | | (unknown) |
| 89: /dev/disk/flopp1lc | | 3.5 floppy | fdi0-unit-0 |
| 102: /dev/disk/cdromic | COMPAQ | CRD-8402B | bus-0-targ-0-lun-0 |
| 103: /dev/disk/dsk8c | COMPAQ | BB009235B6 | bus-2-targ-0-lun-0 |
| 104: /dev/disk/dsk9c | COMPAQ | BB009235B6 | bus-2-targ-1-lun-0 |
```

## 第 12 章 独立系统 TruCluster 服务器![](img/81b0644c1716280bf49aad49627d_31_0.png)图 12-2: 硬件和设备特殊数据库位置

#### /etc 中的硬件和设备特殊文件

| Database | Cluster | Standalone | Cluster | Standalone |
| --- | --- | --- | --- | --- |
| dccd.dat | file | dec_hwc_ldb | cdsl* | file |
| dccd.dat | file | dec_scsi_db | cdsl* | file |
| ddr.db | cdsl* | file | dec_unid_db | file |
| ddr_db | cdsl* | file | dfsc.dat | file |
| dec_dev_db | cdsl* | file | dfsl.dat | cdsl | cdsl |
| dec_hw_db | cdsl* | file | gen_databases | cdsl* | file |
| dec_hwc_cdb | file | | | |

表 12-2: /etc 中的硬件和设备特殊文件
