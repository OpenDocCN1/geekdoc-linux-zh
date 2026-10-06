
# RAID0

`RAID0` 不提供冗余。这意味着如果一个磁盘故障，所有数据将会丢失。

`GEOM` 磁盘子系统提供了磁盘条带化的软件支持，也称为 `RAID0`，且无需 `RAID` 磁盘控制器。

在 `RAID0` 中，数据被分成若干块并跨写入阵列中的所有驱动器中。如下图所示，`RAID0` 无需等待系统向单个磁盘写入 256k，而是同时向阵列中的四个磁盘的每个磁盘写入 64k，从而提供了卓越的 I/O 性能。通过多个磁盘控制器可以进一步增强这种性能。

`RAID0` 不提供冗余。这意味着如果阵列中的一个磁盘故障，所有数据将会丢失。

## 在 FreeBSD 系统中创建条带

1. 加载 `geom_stripe` 模块：
```bash
kld geom_stripe
```

2. 确保存在一个挂载点。

3. 确定磁盘名称，并创建条带化的磁盘：
```bash
stripe -v ad2 ad3
```

4. 在条带上写入标签：
```bash
echo "/dev/stripe0s1 /mnt ufs 0 0" >> /etc/fstab
```

5. 在系统初始化时自动挂载条带，使用 `UFS` 格式化条带化磁盘：
```bash
newfs -U /dev/stripe0s1
```

6. 手动挂载条带：
```bash
mount /dev/stripe0s1
```

7. 在 `/etc/fstab` 中添加条带信息：
```bash
echo "/dev/stripe0s1 /mnt ufs 0 0" >> /etc/fstab
```

8. 通过修改 `/boot/loader.conf` 自动加载 `geom_stripe` 模块：
```bash
echo 'geom_stripe_load="YES"' >> /boot/loader.conf
```

# RAID1 - 镜像

`RAID1`，或者镜像，是将相同的数据写入多个驱动器的技术。镜像通常用于防止驱动器故障导致的数据丢失。镜像中的每个驱动器都包含数据的副本。当某个驱动器故障时，镜像可以继续工作，管理员有时间在不中断用户的情况下更换驱动器。

这些示例展示了两种常见情况：使用两个新驱动器创建镜像并将其作为现有驱动器的替代；第二个示例是在单个新驱动器上创建镜像，将旧驱动器的数据复制进去，然后将旧驱动器插入镜像。这种方法可以从仍然运行的驱动器提供数据。

## 19.3.1. 元数据问题

许多磁盘系统在磁盘末尾存储元数据。在重用磁盘之前，应该清除元数据。大多数问题是由两种特定的遗留元数据引起的：`GPT` 分区表和之前的镜像元数据。

可以使用 `gpart(8)` 清除 `GPT` 元数据：
```bash
# gpart destroy -F ada8
```

### 使用两个新磁盘创建镜像

可以使用 `gmirror(8)` 从活动镜像中移除磁盘并擦除元数据。示例如下：
```bash
# mirrorir remove gm4 ada8
```
如果镜像没有运行，但磁盘上仍有旧的镜像元数据，使用 `mirrorir clear` 将移除：
```bash
# mirrorir clear ada8
```
`gmirror(8)` 在磁盘末尾存储一个元数据块。由于 `GPT` 分区方案也在磁盘末尾存储元数据，因此不建议使用 `gmirror(8)` 镜像整个 `GPT` 磁盘。

从原始 `ada0` 磁盘的文件系统现在可以使用 `dump(8)` 和 `restore(8)` 复制到镜像上。

```
# mount /dev/mirror/gm0s1a /mnt
```

```
# dump -C16 -b64 -0aL -f - | (cd /mnt && restore -rf -)
```

```
# mount /dev/mirror/gm0s1d /mnt/var
```

```
# mount /dev/mirror/gm0s1e /mnt/tmp
```

```
# mount /dev/mirror/gm0s1f /mnt/usr
```

```
# dump -C16 -b64 -0aL -f /var | (cd /mnt/var && restore -rf -)
```

```
# dump -C16 -b64 -0aL -f /tmp | (cd /mnt/tmp && restore -rf -)
```

```
# dump -C16 -b64 -0aL -f /usr | (cd /mnt/usr && restore -rf -)
```

编辑 `/mnt/etc/fstab` 以指向新的镜像系统：

| Device | Mountpoint | FType | Options | Dump | Pass |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/mirror/gm0s1a | / | ufs | rw | 1 | 1 |
| /dev/mirror/gm0s1b | none | swap | sw | 0 | 0 |
| /dev/mirror/gm0s1d | /var | ufs | rw | 2 | 2 |
| /dev/mirror/gm0s1e | /tmp | ufs | rw | 2 | 2 |
| /dev/mirror/gm0s1f | /usr | ufs | rw | 2 | 2 |

如果 `geom_mirror.ko` 内核模块尚未编译进内核中，则编辑 `/mnt/boot/loader.conf` 在启动时加载该模块：

```
geom_mirror_load="YES"
```

重启系统以测试新镜像并验证所有数据均已复制。`BIOS` 将镜像视为两个独立的驱动器，而不是镜像。由于驱动器是相同的，选择哪一个启动都重要。

如果启动时出现问题，请参见第 19.3.4 节“故障排除”。关机并断开原始 `ada0` 磁盘可以将其作为离线备份。

在使用时，镜像的行为将与原始单驱动器完全相同。

## 19.3.3. 使用现有驱动器创建镜像

在本示例中，`FreeBSD` 已经安装在单磁盘 `ada0` 上。一个新磁盘 `ada1` 已连接到系统。将在新磁盘上创建一个单磁盘镜像，将现有系统复制到其中，然后将旧磁盘插入镜像中。需要这一稍显复杂的程序是因为 `gmirror` 需要在每个磁盘的末尾放置一个 512 字节的元数据，而现有的 `ada0` 的所有空间已经被分配完毕。

加载 `geom_mirror.ko` 内核模块：
```
# gmirror load
```

使用 `diskinfo` 检查原始磁盘的媒体大小：
```
# diskinfo -v ada0 | head -n3
```
/dev/ada0
```
512 # sectorsize
1000204821504 # mediasize in bytes (931G)
375
```

### 使用现有驱动器创建镜像

在新磁盘上创建镜像。为了确保镜像容量不大于原始 `ada0` 驱动器，使用 `gnop(8)` 创建一个具有完全相同大小的假驱动器。该驱动器不存储任何数据，仅用于限制镜像的大小。当 `gmirror(8)` 创建镜像时，它将容量限制为 `gzero.nop` 的大小。请注意，第二行中的 `1000204821504` 等于上述 `diskinfo` 所示的 `ada0` 媒体大小。
```
# geom zero load
# gnop create -s 1000204821504 gzero
# gmirror label -v gm0 gzero.nop ada1
# gmirror forget gm0
```
由于 `gzero.nop` 不存储任何数据，镜像不会认为其为已连接。镜像被告知“遗忘”未连接的组件，从而移除对 `gzero.nop` 的引用。结果是一个仅包含单个磁盘 `ada1` 的镜像设备。

创建 `gm0` 后，查看 `ada0` 上的分区表。此输出来自一个 1 TB 的驱动器。如果磁盘末尾有一些未分配的空间，则可以直接从 `ada0` 将内容复制到新镜像。

然而，如果输出显示磁盘上的所有空间已分配（如下列表所示），则磁盘末尾没有空间为 512 字节的镜像元数据提供空间。
```
# gpart show ada0
=> 63 1953525105 ada0 MBR (931G)
63 1953525105 1 freebd [active] (931G)
```
在这种情况下，必须编辑分区表，以将镜像/`gm0` 的容量减少一个扇区。该将在稍后解释。

无论何种情况，主磁盘上的分区表都应首先使用 `gpart backup` 复制：
```
# gpart backup ada0
# gpart backup ada1
```
这两个命令创建了 `ada0` 和 `ada1`。此示例来自一个 1 TB 的驱动器：
```
# gpart show ada0
```
使用 `gpart show` 查看分区表。
```
# gpart show ada1
```
如果磁盘末尾有未分配的空间，则镜像/`gm0` 的切片和最后一个分区必须减少一个扇区。该程序将在稍后解释。

使用 `gpart restore` 优先恢复主磁盘上的分区表：
```
# gpart restore ada0
# gpart restore ada1
```

| 名称 | 状态 | 组件 |
| :--- | :--- | :--- |
| mirror/gm0 | 降级 (DEGRADED) | ada1 (ACTIVE) |
| | ada0 (同步中, 64%) |

过了一段时间，同步将完成。

`GEOM_MIRROR`: 设备 `gm0`: 重新构建程序 `ada0` 完成。
```bash
# gmirror status
```

| 名称 | 状态 | 组件 |
| :--- | :--- | :--- |
| mirror/gm0 | 完成 (COMPLETE) | ada1 (ACTIVE) |
| | ada0 (ACTIVE) |

`mirror/gm0` 现在由 `ada0` 和 `ada1` 两个磁盘组成，其内容会自动相互同步。在使用时，`mirror/gm0` 的行为将与原始单驱动器相同。

## 19.3.4. 故障排除

如果系统不再启动，可能需要更改 `BIOS` 设置以从新的镜像驱动器之一进行启动。任何一个驱动器都可以用于启动，因为它们包含相同的数据。

如果启动停止并显示此消息，则镜像设备出现某种问题：

从 `ufs:/dev/mirror/gm0s1a` 挂载失败，错误 19。

加载器变量：
```bash
vfs.root.mountfrom=ufs:/dev/mirror/gm0s1a
```
```bash
vfs.root.mountfrom.options=rw
```
378

第19 章，`GEOM`: 模块化磁盘转换框架

手动根文件系统指定：

`<fstype>:<device> [options]`

使用文件系统 `<fstype>` 挂载 `<device>` 并使用指定的（可选）选项列表。

例如 `ufs:/dev/da0s1a`
`zfs:tank`
`cd9660:/dev/acd0`
（等同于：`mount -t cd9660 -o ro /dev/acd0 /`）

? 列出有效的启动设备
等待 1 秒（用于后台任务）
<空行> 取消手动输入

`mountroot>`

在 `/boot/loader.conf` 中忘记加载 `geom_mirror.ko` 模块可能会导致此问题。要修复它，请从 `FreeBSD` 安装媒体启动并在第一个提示处选择 Shell。然后加载镜像模块并挂载镜像设备：
```bash
# gmirror load
```
```bash
# mount /dev/mirror/gm0s1a/mnt
```
编辑 `/mnt/boot/loader.conf`，添加一行来加载镜像模块：
```bash
geom_mirror_load="YES"
```
保存文件并重启。

导致错误 19 的其他问题需要更多努力来修复。虽然系统应该从 `ada0` 启动，但如果 `/etc/fstab` 错误，会出现另一个选择 shell 的提示。在加载器提示符处输入 `ufs:/dev/ada0s1` 并按回车。撤销对 `/etc/fstab` 的编辑，然后从原始磁盘（`ada0`）而不是镜像挂载系统。重启系统并再次尝试该过程。

输入 shell 的完整路径或按 RETURN 使用 `/bin/sh`：
```bash
# cp /etc/fstab.orig /etc/fstab
```
```bash
# reboot
```

## 19.3.5. 从磁盘故障中恢复

磁盘镜像的好处是，单个磁盘故障不会导致镜像丢失任何数据。在上面的示例中，如果 `ada0` 失败，镜像将继续工作，从剩余的工作驱动器 `ada1` 提供数据。

要替换故障的驱动器，请关闭系统并用相等或更大容量的新驱动器物理替换故障驱动器。制造商在以 GB 为单位评估磁盘时使用相当任意的值，唯一真正确定的方法是比较 `diskinfo -v` 显示的扇区总数。容量大于镜像的驱动器可以工作，尽管新磁盘上的额外空间将不会被使用。

电脑重新电源后，镜像将以“降级”模式运行，只有一个驱动器。告诉镜像忘记当前未连接的驱动器：
```bash
# gmirror forget gm0
```
应根据第 19.3.1 节“元数据问题”中的说明从替换磁盘清除任何旧元数据。然后将替换磁盘（在此例中 `ada4`）插入镜像：
```bash
# gmirror insert gm0 /dev/ada4
```
