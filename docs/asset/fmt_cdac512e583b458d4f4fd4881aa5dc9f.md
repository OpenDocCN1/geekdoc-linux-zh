
[root@fedora-server ~]# `pvdisplay`

--- Physical volume ---

PV Name `/dev/sda3`

VG Name `Volgroup`

PV Size 78.12 GiB / not usable 32.00 MiB

<OUTPUT TRUNCATED>...

```

请注意物理卷名称字段 (`PV Name`)。

### 3. 使用 `pvcreate` 命令将我们在上一节（“创建分区”）中创建的分区初始化为物理卷：

```
[root@fedora-server ~]# `pvcreate` `/dev/sda4`

Physical volume "/dev/sda4" successfully created
```

### 4. 使用 `pdisplay` 命令查看你的更改：

```
[root@fedora-server ~]# `pdisplay`

--- Physical volume ---

PV Name `/dev/sda3`

VG Name `VolGroup`

<OUTPUT TRUNCATED>...

"/dev/sda4" is a new physical volume of "19.04 GiB"

--- NEW Physical volume ---

PV Name `/dev/sda4`

VG Name

PV Size 19.04 GiB

<OUTPUT TRUNCATED>...
```

## 将物理卷分配给卷组 (Volume Group)

在这里，我们将之前创建的物理卷分配给一个卷组 (`VG`)。

### 1. 首先，使用 `vgdisplay` 命令查看系统上可能存在的当前卷组：

```
[root@fedora-server ~]# `vgdisplay`

Volume group ---

VG Name             VolGroup

System ID

Format              lvm2

  <OUTPUT TRUNCATED>...

VG Size             78.09 GIB

PE Size             32.00 MiB

Total PE            2499

Alloc PE / Size     2499 / 78.09 GIB

Free PE / Size      0 / 0

VG UUID             e3MLE-X36P-z4UF-Vuac-srJx-9iCo-8qwbqz
```

从前面的输出中，我们可以看到以下内容：
- 组名 (`VG Name`) 为 `VolGroup`。
- VG 的当前大小为 78.09 GIB（在我们完成后这个值会增加）。
- 物理大小为 32 MiB，总共有 2499 个 PE。
- VG 中没有空闲的物理区（physical extents）。

### 2. 使用 `vgextend` 命令将新 PV 分配给卷组。该命令的语法为：
`vgextend [options] VolumeGroupName PhysicalDevicePath`
在命令中替换为正确的值，输入输入：

```
[root@fedora-server ~]# `vgextend` `VolGroup` `/dev/sda4`

Volume group "VolGroup" successfully extended
```

### 3. 使用 `vgdisplay` 命令查看你的更改：

```
[root@fedora-server ~]# `vgdisplay`

Volume group ---

VG Name             VolGroup

  <OUTPUT TRUNCATED>...

Act PV              

VG Size             97.12 GIB

PE Size             32.00 MiB

Total PE            3108
```

Alloc PE / Size 2499 / 78.09 GiB
Free PE / Size 609 / 19.03 GiB
VG UUID e3MLey-X36P-z4UF-VUac-srJx-9io-8wbz

注意 `VG Size`、`Total PE` 和 `Free PE` 值已大幅增加。我们现在拥有 609 个空闲 PE（或 19.03 GiB）。

## 创建逻辑卷 (Logical Volume)

现在 VG 中有了空间，我们可以开始创建逻辑卷了。

首先查看系统上当前的 LV：

```
[root@fedora-server ~]# `lvdisplay` | `less`

  -- Logical volume             /dev/VolGroup/LogVol01

  VG Name                       VolGroup

  <OUTPUT TRUNCATED>...

  -- Logical volume             /dev/VolGroup/LogVol00

  VG Name                       VolGroup

  <OUTPUT TRUNCATED>...

  -- Logical volume             /dev/VolGroup/LogVol03

  VG Name                       VolGroup

  <OUTPUT TRUNCATED>...

  -- Logical volume             /dev/VolGroup/LogVol02

  VG Name                       VolGroup

  <OUTPUT TRUNCATED>...
```

上述输出显示了当前的 LV：
* `/dev/VolGroup/LogVol01`
* `/dev/VolGroup/LogVol00`
* `/dev/VolGroup/LogVol03`
* `/dev/VolGroup/LogVol02`

有了这些背景信息，我们将使用系统相同的命名约定创建一个 LV。我们将创建一个名为 "`LogVol04`" 的第五个 LV。LV 的完整路径为 `/dev/VolGroup/LogVol04`。输入：

```
[root@fedora-server ~]# `lvcreate` -l 609 --name `LogVol04` `VolGroup`

Logical volume "LogVol04" created
```

> 注意：你实际上为 LV 命名任何名称。我们只是为了一致性而命名为 `LogVol04`。如果需要，可以将 `LogVol04` 替换为 "`my-volume`"。`--name` 参数决定 LV 的名称。`-L` 选项指定物理区的大小。我们可以通过 `-L 19.03G` 或 `-L 1903M` 等选项指定 GB 或 MB 大。

### 3. 查看你创建的 lv：

```
[root@fedora-server ~]# `lvs` `/dev/VolGroup/LogVol04`

--------------------

LV Name               /dev/VolGroup/LogVol04

VG Name               VolGroup

  <OUTPUT truncated>...

LV Size               19.03 GiB

Current LE           609

Segments             1

Allocation           inherit

Read ahead auto set to 256

Block device          4
```
