
`../devices/iommu/e0000000/sbus/e0001000/espmaff/400000/espf/sd@0,f`

在 `ls -l` 命令输出的第二行中，注意逻辑设备名称 `c0t0d00` 链接到物理设备名称：

```
../devices/iommu/\sbus \
@f,e0001000/espmaff/400000/espf/sd@0,a
```

逻辑设备名称是系统管理员在运行 Solaris 文件系统命令时，引用特定设备时使用的名称。例如，如果运行 `mount` 命令来挂载文件系统 `/home`，使用逻辑设备名称 `/dev/dsk/c0t0d0s7`：

```
mount /dev/dsk/c0t0d0s7
```

# 第 16 章 设备管理与磁盘管理 581

`/dev` 目录中的逻辑设备文件符号链接到 `/devices` 目录中的物理文件。如果执行以下操作，则使用逻辑设备名称来访问磁盘设备：

- 向系统添加新磁盘。
- 将磁盘从一个系统移动到另一个系统。
- 访问（或挂载）位于本地磁盘上的文件系统。
- 备份本地文件系统。
- 修复文件系统。

逻辑设备根据其设备类型组织在 `/dev` 目录下的子目录中，所示：

| 表 16.3 目录 | 内容 |
| :--- | :--- |
| `/dev/dsk` | 块设备 |
| `/dev/rdsk` | 字符设备 |
| `/dev/rmt` | 磁带 |
| `/dev/term` | 串行 |
| `/dev/cua` | 拨号器 |
| `/dev/pts` | 伪终端 |
| `/dev/fb` | 帧 |

## 块设备与原始设备

磁盘驱动器在 `/dsk` 和 `/rdsk` 目录中都有项。`/dsk` 目录指向缓冲设备，而 `/rdsk` 目录指向字符设备文件。`rdsk` 中的“r”代表“raw”。如果你熟悉这些设备，请参阅第 3 章，“安装 Solaris 软件”。

第 II 部分 `/dsk` 目录包含 `/devices` 中的块设备节点项，如下所示所示：

```
ls -l /dev/dsk

total 48

lrwxrwxrwx 1 root root 84 Jul 21 07:45 c0t0d00 -> \
../devices/iommu/e0000000/sbus/e0001000/espmaff/400000/espf/sd@0,a

lrwxrwxrwx 1 root root 84 Jul 21 07:45 c0t0d01 -> \
../devices/iommu/e0000000/sbus/e0001000/espmaff/400000/espf/sd@0,b

lrwxrwxrwx 1 root root 84 Jul 21 07:45 c0t0d02 -> \
../devices/iommu/e0000000/sbus/e0001000/espmaff/400000/espf/sd@0,c

...
```

`/rdsk` 目录包含 `/devices` 中的字符设备节点项，如下所示所示：

```
ls -l /dev/dsk

lrwxrwxrwx 1 root root 84 Jul 21 07:45 c0t0d00 -> \
../devices/iommu/e0000000/sbus/e0001000/espmaff/400000/espf/sd@0,a
...
```
