
```
$ vgdisplay /dev/vg00

--- Volume groups ---

VG Name /dev/vg00

VG Write Access read/write

VG Status available

Max LV 255

Cur LV 7

Open LV 7

Max PV 16

Cur PV 1

Act PV 1

Max PE per PV 2000

VGDA 2

PE Size (Mbytes) 4

Total PE 157

Alloc PE 149

Free PE 8

Total PVG 0
```

## vgexport

此命令从系统中删除一个逻辑卷组，但不会修改物理卷上的逻辑卷信息。这些物理卷随后可以使用 `vgimport` 导入到另一个系统。

## vgextend

可以使用此命令通过指定要添加到卷组的物理卷，将物理卷添加到卷组。

## vgimport

此命令可用于将物理卷导入到另一个系统。

## vgreduce

可以使用此命令通过指定要从卷组删除的物理卷来减小卷组的大小。在执行此操作之前，请确保要删除的物理卷上没有数据。

## vgremove

可以使用此命令从系统中完全删除卷组定义。

## vgscan

在发生某种类型的灾难时，你可以使用此命令扫描系统，尝试重建 `/etc/lvmtab` 文件。

## vgsync

卷组中的镜像数据有时会变得“过时”或过更新。`vgsync` 用于同步卷组中每个镜像逻辑卷的物理区。

## 逻辑卷命令

## lvcreate

此命令用于创建新的逻辑卷。逻辑卷创建在卷组内部。逻辑卷可以跨越多个磁盘，但必须存在于卷组中。当你使用 SAM 创建逻辑卷时，SAM 会为你执行此命令。此命令有许多选项，你经常会使用的两个是 `-L` 用于定义逻辑卷的大小，`-n` 用于定义逻辑卷的名称。

## lvchange

此命令用于某种方式更改逻辑卷。例如，你可能希望 `-p` 选项将逻辑卷的权限更改为读写 (`w`) 或只读 (`r`)。或者你可能想将严格策略（在“磁盘镜像”下描述）更改为严格 (`y`)、不严格 (`n`) 或 PVG 严格 (`g`)。

## lvdplay

此命令显示你指定的每个逻辑卷的状态和特征。如果你使用此命令的详细 (`-v`) 选项，你将在许多类别中获得大量有用数据，包括：

- 1) 关于逻辑卷设置方式的信息，例如出现逻辑区所在的物理卷；物理卷上本地区（local extents）的数量；以及该物理卷上物理区的数量。
- 2) 逻辑区的详细信息，包括逻辑区编号以及关于该逻辑区的物理卷和物理区的一些信息。

以下是之前的 bdf 示例中显示的第一个逻辑卷 (`lvol1`) 的 `lvdplay` 示例：

```
$ lvdplay -v /dev/vg00/lvol1

--- Logical volumes ---

LV Name             /dev/vg00/lvol1

VG Name             /dev/vg00
```
