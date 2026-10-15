
如前一节所述，要恢复 `cluster_root`，您必须拥有一个可引导的非集群操作系统盘，其操作系统版本和补丁级别与当前集群相同。我们的建议是，当您在集群上安装补丁包时，始终将补丁包 `tar(1)` 文件复制到 Emergency Repair（ER）盘上的文件系统；这样如果需要时您就能找到它。您可能会问 Emergency Repair 盘是什么？它就是您最初用来构建操作系统并从中运行 `clu_create(8)` 的盘。我们建议在安装后保留该盘和操作系统文件系统不变。

## 22.2.1.4 Replacing a Member Disk

如果您只需要更换一个成员盘，并且拥有“a”分区的 `vdump`，您可以恢复该盘或将数据恢复到新盘。以下流程中，您可以跳过任何“纠正”我们正在恢复到已为集群所知的不同盘这一事实的步骤（这些步骤会用“†”标记）。有关向系统添加磁盘的更多信息，请参阅第 7.4.4 节。我们的原始配置中 `molari`（`member1`）的成员引导盘为 `dsk2`，其替换盘为 `dsk10`。除非另有说明，所有步骤均在集群的已启动成员上执行。

- 1. 确保具有故障引导盘的成员已关闭。

```
# clu_get_info -m 1
```

- 2. 将 `dsk10` 设置为 `member 1` 的引导盘。

```
# /usr/sbin/clu_bdmgr -o dsk10 1
```

如果 `dsk10` 不是 `molari` 的原始引导盘，您将收到警告信息，并会看到将 `/etc/sysconfigtab` 文件更改为反映此更改的说明†。记下这些更改。它们看起来会像这样：

```
The new member's disk, dsk10, is not the same name as the original disk configured for domain root1_domain. If you continue the following changes will be required in member1's /etc/sysconfigtab file:
vm:
swapdevice=/dev/disk/dsk10b
clubase:
cluster_seqdisk_major=19
cluster_seqdisk_minor=195
```

- 3. 挂载 `molari` 的新引导盘 `root domain`。 （`clu_bdmgr` 命令创建了 `domain` 和 `fileset`。）

```
# mount root1_domain@root /mnt
```

- 4. 恢复成员的 `boot_partition`。

```
# vrestore -xf /dev/tape/tape0 -D /mnt
```

- 5. 根据步骤 2 中的早期说明修改 `/etc/sysconfigtab` 以反映新盘（`dsk10`）。提取现有成员的 `clubase` 和 `vm` 部分到一个 `stanza` 文件中：

```
# sysconfigdb -t /mnt/etc/sysconfigtab -l clubase vm > /tmp/bd.mod.stanza
```

编辑 `stanza` 文件：

```
# vi /tmp/bd.mod.stanza
```

使其如下：

```sh
# sysconfigtab -t /mnt/etc/sysconfigtab -a -f /tmp/bd_mod.stanza.vx
# sysconfigtab -t /mnt/etc/sysconfigtab -m -f /tmp/bd_mod.stanza clauses
```

- 6. 恢复“n”分区（`cnx`）。

```sh
# /usr/sbin/clu_bdmgr -h dsk10
```

- 7. 卸载成员的 `boot_partition`。

```sh
# umount /mnt
```

- 8. 在 `molari` 的控制台上调整 `bootdef_dev` 控制台变量以反映更改。

```text
>>> set bootdef_dev DKB202
```

设备 `DKB202` 是在 UNIX 中对应 `dsk10` 的适当控制台设备名称。

- 9. 启动 `molari`。

```text
>>> boot
```

## 22.1.5 Restoring a Critical Data File System

正如文件系统丢失对操作系统至关重要一样，关键数据文件系统的丢失也可能成为集群的问题。恢复数据或非 OS 文件系统在集群中与在独立的 Tru64 UNIX 系统中其实并无不同。例如，如果您的备份使用 `vdump` 制作，您就可以使用以下 `vrestore` 命令轻松恢复它们：

```sh
# vrestore -xf /dev/tape/tape0 -D /data
```

如果恢复到新盘，您当然必须先对其进行 `disklabel` 并创建新的文件系统（AdvFS 或 UFS），然后再进行恢复，并重命名设备特殊文件或调整对设备名称的任何引用（如在 `/etc/fdmns` 中）以指向新设备。关键在于，这并不是因为它是集群而变得特殊。

## 22.2 更换 HBA 和/或 HSx 控制器

在集群的生命周期中，你可能会遇到某些硬件故障，而这些本身并不是大问题，因为你的集群已配置为无单点故障（NSPOF）。处理这些维护项目通常只需要一点思考，然后集群就会继续愉快地运行。

### 22.2.1 更换 HSG80 控制器

在大多数情况下，如果你遇到存储控制器故障，例如 HSG80，通常一次只会有一对双控制器中的一个发生故障。在这种情况下，WWID 发生变化的前景不是问题；它会被剩余的控制器接管，并在更换故障控制器后得以保留。然而，如果你遇到双重故障或其他导致 WWID 被销毁的故障，则必须能够在 HSG80 上重置 WWID。你可以通过 HSG80 控制台上的单个命令来完成此操作。

```
HSG80> set this wwn=5000-1FE1-0000-9630
```

在这种情况下，“5000-1FE1-0000-9630”是 WWID，“YO”是校验和。你可以从 HSG80 控制器获取这两个值。这些值位于设备上，而非可更换的控制器本身，而是位于 HSG80 机箱的更永久部件上。

### 22.2.2 更换 HSZ70 控制器

如果你的控制器是双 `HSZ70`（透明故障转移或多总线故障转移），并且发生单次故障，只要在另一个出现问题之前更换故障控制器，你就没问题。如果你不幸遇到双重故障（这种情况极其罕见），那么你将不得不使用 `dsmgr(8)` 做一些工作，以将磁盘名称恢复到之前的状态。这就是我们建议保留第 21 章中提到的文件和命令输出的原因之一。此外，拥有最新的、已修补的 HSOF 软件非常重要。对于此过程正常工作，你的 HSZx0 至少应达到以下补丁级别：

- `HSZ40`：V37Z-1。

- `HSZ50`：V57Z-1。

- `HSZ70`：V77Z-1。

在继续操作之前，请熟悉这些 HSOF 命令。如果使用不当，它们可能会导致数据丢失。

- `set nofailover`

- `set failover copy=this`

- `set multibus_failover copy=this`

#### 22.2.2.1 HSZ70 在透明故障转移模式下

此过程适用于 `HSZ70`，也适用于配置为透明故障转移模式的 `HSZ40` 和 `HSZ50` 控制器。操作系统必须启动以处理控制器更改。如果尚未启动，至少必须启动到单用户模式。

1. 从正在运行的操作系统开始（受影响 `HSZx0` 上的设备应存在并可见）。

2. 在连接到正常工作的控制器的情况下，在 `HSZx0` 上发出 `set nofailover` 命令。

3. 当绿色 LED 状态灯不再闪烁时，移除故障控制器。

4. 在每个成员上使用 `hwmgr -scan scsi -bus N`（其中“N”是与该 `HSZx0` 关联的总线号）扫描总线，或使用我们的 `clu_scan_scsi` 脚本（这将使我们注意到从双控制器到单控制器的变化）。

   你可能会在 `HSZx0` 控制台上看到几条“was dual, now single”消息。

   尽管 `hwmgr` 命令执行后提示符会很快返回，但扫描仅被启动。在进行下一步之前，请给扫描大约一分钟时间完成。

5. 更换故障控制器。

6. 再次使用 `hwmgr -scan scsi -bus N` 扫描总线。

7. 发出 `set failover copy=this` 命令（在连接到原始正常控制器时）。

   你应该会在 `HSZx0` 控制台上看到几条“upgraded to dual”消息。

8. 最后一次使用 `hwmgr -scan scsi -bus N` 或 `clu_scan_scsi` 扫描总线（这将使我们注意到从单控制器恢复到新的双冗余对的变化）。

#### 22.2.2.2 HSZ70 在多总线故障转移模式下

此过程需要对 TruCluster Server 版本 5.1A 或 5.1B 进行修补。截至本文撰写时，该补丁尚未包含在聚合补丁包中。
