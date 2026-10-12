
```
[root@RHEL5 ~]# pvcreate /dev/sdc1
Physical volume "/dev/sdc1" successfully created
[root@RHEL5 ~]#
```

你也可以向`pvcreate`添加多个磁盘或分区。此示例向`lvm`添加了三个磁盘。

```
[root@RHEL5 ~]# pvcreate /dev/sde /dev/sdf /dev/sdg
Physical volume "/dev/sde" successfully created
Physical volume "/dev/sdf" successfully created
Physical volume "/dev/sdg" successfully created
[root@RHEL5 ~]#
```

### 2. `pvremove`

使用`pvremove`命令从`lvm`中移除物理卷。这些设备可能在使用中。

```
[root@RHEL5 ~]# pvremove /dev/sde /dev/sdf /dev/sdg
Labels on physical volume "/dev/sde" wiped
Labels on physical volume "/dev/sdf" wiped
Labels on physical volume "/dev/sdg" wiped
[root@RHEL5 ~]#
```

### 3. `pvresize`

当你使用`fdisk`调整磁盘上的分区大小时，使用`pvresize`让`lvm`识别该物理卷的新大小。

```
[root@RHEL5 ~]# pvresize /dev/sde1
Physical volume "/dev/sde1" changed
1 physical volume(s) resized
0 physical volume(s) not resized
```

### 4. `pvchange`

通过`pvchange`可以防止在新的卷组或逻辑卷中分配物理卷。这在你计划移除物理卷时非常有用。

```
[root@RHEL5 ~]# pvchange -xn /dev/sdd
Physical volume "/dev/sdd" changed
1 physical volume changed
0 physical volumes not changed
[root@RHEL5 ~]#
```

为了恢复之前的设备，此示例显示了如何重新启用物理卷以允许分配。

```
[root@RHEL5 ~]# pvchange -xy /dev/sdd
Physical volume "/dev/sdd" changed
1 physical volume changed
0 physical volumes not changed
[root@RHEL5 ~]#
```

### 5. `pvmove`

通过`pvmove`你可以将卷组内的逻辑卷移动到另一个物理卷。这必须在移除物理卷之前完成。

```
[root@RHEL5 ~]# pvs | grep vg1
/dev/sdf vg1 lm2- 816.00M 0
/dev/sdg vg1 lm2- 816.00M 816.00M
[root@RHEL5 ~]# pvmove /dev/sdf
/dev/sdf: Moved: 70.1%
/dev/sdf: Moved: 100.0%
[root@RHEL5 ~]# pvs | grep vg1
/dev/sdf vg1 lm2- 816.00M 816.00M
/dev/sdg vg1 lm2- 816.00M
```

## 12.12. 管理卷组

### 1. `vgcreate`

使用`vgcreate`命令创建卷组。你可以立即命名所有跨越卷组的物理卷。

```
[root@RHEL5 ~]# vgcreate vg42 /dev/sde /dev/sdf
Volume group "vg42" successfully created
[root@RHEL5 ~]#
```

### 2. `vxtend`

使用`vxtend`命令通过物理卷扩展现有卷组。

```
[root@RHEL5 ~]# vxtend vg42 /dev/sdg
Volume group "vg42" successfully extended
[root@RHEL5 ~]#
```

### 3. `vgremove`

使用`vgremove`命令从`lvm`中移除卷组。卷组可能在使用中。

```
[root@RHEL5 ~]# vgremove vg42
Volume group "vg42" successfully removed
[root@RHEL5 ~]#
```

### 4. `vgreduce`

使用`vgreduce`命令从`vg1`卷组中移除物理卷`/dev/sdg`。此示例显示了如何使用`vgextend`将`/dev/sdg`添加`vg1`卷组，然后使用`vgreduce`将其移除。

```
[root@RHEL5 ~]# pvs | grep vg1
/dev/sdg vg1 lm2- 19.20M 19.20M
[root@RHEL5 ~]# vxtend vg1 /dev/sdg
Volume group "vg1" successfully extended
[root@RHEL5 ~]# pvs | grep vg1
/dev/sdg vg1 lm2- 816.00M 816.00M
[root@RHEL5 ~]# vgreduce vg1 /dev/sdg
Removed "/dev/sdg" from volume group "vg1"
[root@RHEL5 ~]# pvs | grep vg1
/dev/sdg vg1 lm2-- 19.20M 19.20M
```

### 5. `vgchange`

使用`vgchange`命令更改卷组的参数。此示例显示了如何防止物理卷添加或移除到卷组`vg1`。

```
[root@RHEL5 ~]# vgchange -xn vg1
Volume group "vg1" successfully changed
[root@RHEL5 ~]# vxtend vg1 /dev/sd5
Volume group vg1 is not resizable.
```

你也可以使用`vgchange`更改卷的其他属性。此示例更改了`vg1`可以提供的最大逻辑卷数量和物理卷数量。

```
[root@RHEL5 ~]# vgdisplay vg1 | grep -i max
Max LV              0
Max PV              0
[root@RHEL5 ~]# vgchange -l16 vg1
Volume group "vg1" successfully changed
[root@RHEL5 ~]# vgchange -p8 vg1
Volume group "vg1" successfully changed
[root@RHEL5 ~]# vgdisplay vg1 | grep -i max
Max LV              16
Max PV              8
```

### 6. `vgmerge`

合并卷组到一个卷是通过`vgmerge`完成的。此示例将`vg2`合并到`vg1`，保留`vg1`的所有属性。

```
[root@RHEL5 ~]# vgmerge vg1 vg2
Volume group "vg2" successfully merged into "vg1"
[root@RHEL5 ~]#
```

## 12.13. 管理逻辑卷

### 12.13.1. `lvcreate`

使用`lvcreate`命令在卷组（Volume Group）中创建逻辑卷。这会在卷组`vg42`中创建一个 8GB 的逻辑卷。

```
[root@RHEL5 ~]# # lvcreate -L5G vg42
Logical volume "lvol10" created
[root@RHEL5 ~]#
```

如你所示，`lvm`会自动创建逻辑卷`Ivol0`。下一个示例在卷组`vg42`中创建一个名为`MyLV`的 200MB 逻辑卷。

```
[root@RHEL5 ~]# lvcreate -L200M -n MyLV vg42
Logical volume "MyLV" created
[root@RHEL5 ~]#
```

下一个示例执行相同的操作，但使用了不同的语法。

```
[root@RHEL5 ~]# lvcreate -size 200M -n MyLV vg42
Logical volume "MyLV" created
[root@RHEL5 ~]#
```

此示例创建了一个占用卷组 10% 空间的逻辑卷。

```
[root@RHEL5 ~]# lvcreate -l 10%VG -n MyLV vg42
Logical volume "MyLV2" created
[root@RHEL5 ~]#
```
