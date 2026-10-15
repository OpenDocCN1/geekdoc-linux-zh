
这是一种经典方法。你通过回环设备（loop devices）挂载取证镜像以访问内部文件。使用常用的 UNIX 命令 `find`、`grep`、`awk`、`strings`、`hexdump`，你可以搜索文件系统检索你需要的所有数据。

你并不能真的称之为“取证检查”，但嘿——这只是入门工具包，对吧？通过这种方法，你将学习到 80/20 法则（取决于引用的不同，可能是 70/30）。这条取证法则指出，80% 的证据都浮在数据集中，可以使用像这样简单的方法找回。接下来的 10% 将花费双倍的成本才能提取，接下来的 5% 再花费双倍，以此类推……

关键在于识别每个案例中停止的“黄金点”！

# 附录 B：Linux 取证与数据恢复

| 检查清单 | 描述 |
| :--- | :--- |
| 检查镜像分区表。 | 使用回环设备：`losetup /dev/[firstloopdevice] [image_file] sectors`。 |
| 使用 fdisk、sfdisk 或 parted 查看分区表结构。 | 记得检查镜像以查看扇区中的结果。 |
| 在安全模式下挂载镜像。 | `mount -o ro,loop,nodev,user,noexec,notime,of offset=[first_partition_cylinder*512] [image_file] [mount_point]` |
| 执行文件系统分析。 | 搜索并检索分析所需的所有数据（`find`、`grep`、`awk`、`strings`、`hexdump`），检查 rootkit 等。 |
| 搜索日志。 | 使用 `find` 找到文件系统中每一个有趣的日志文件。 |
| 关联日志。 | 使用 `lire`、`optopsy`、`ADLogger`、`sawmill`、`splunk` 或你喜欢的工具来关联日志文件。日志和 MAC 时间关联是你应该采取的第一步，以便了解在特定时间段内系统中发生了什么。 |

# 事后分析 (案例 2)

有时你可能会发现一个未知的文件系统、交换区域或休眠文件，或者你只是想将触角延伸到未分配簇。在这些情况下，你可以使用文件雕刻（file carver）来检索数据。文件雕刻工具是强大的工具，必须小心使用，因为如果你不聪明使用，它们很容易让你被信息淹没。

文件雕刻（File carving）是指通过分析一组信息（通常是大数据集）中已知文件格式的头部（headers）和尾部（footers），以便获取其中的数据并有效地将其“雕刻”出来。这就是名称的由来。

还有其他技术可以增强雕刻效果，你将在不久的将来看到该领域的许多进展；很快，文件雕刻将消耗与密码破解一样多的资源——走着吧……但目前我们先保持简单的头部/尾部雕刻。

在某个时间点，你会开始开发自己的头部和尾部，目前已有工具可以为你自动化这些工作，并允许你检索删除的文档，这对于你正在进行的调查可能有用。

> 请记住一点！并不总是需要把一切都刻出来！如果你知道你在寻找什么，并且知道那段数据在你感兴趣的文件格式中是如何存储的，那就不要雕刻！只需适应目标格式并搜索即可！那样会快得多。

## 黑客攻防 Linux：Linux 安全秘密与解决方案

| 检查清单 | 描述 |
| :--- | :--- |
| 识别文件类型。 | 映射你需要每种文件类型。 |
| 使用文件雕刻工具从文件系统和交换分区提取文件。 | 文件雕刻工具（`foremost` 或 `scalpel`）将检索它能识别每一个每一个（根据你选择的类型）。文件不能碎片。它适用于每个文件系统和交换文件或分区。 |

# 事后分析 (案例 3)

你可能想检查镜像，这可能帮助你发现一个未知的文件系统、交换区域或休眠文件，或者你只是想将范围扩大到未分配簇。在这些场景下，你可以使用文件雕刻工具来检索数据。文件雕刻工具是强大的工具，必须小心使用，因为如果你不聪明使用，它们很容易让你被信息淹没。

文件雕刻（File carving）是指通过分析一组信息（通常是大数据集）中已知文件格式的头部（headers）和尾部（footers），以便获取其中的数据并有效地将其“雕刻”出来。这就是名称的由来。

还有其他技术可以增强雕刻效果，你将在不久的将来看到该领域的许多进展；很快，文件雕刻将消耗与密码破解一样多的资源——走着吧……但目前我们先保持简单的头部/尾部雕刻。

在某个时间点，你会开始开发自己的头部和尾部，目前已有工具可以为你自动化这些工作，并允许你检索删除的文档，这对于你正在进行的调查可能有用。

> 请记住一点！并不总是需要把一切都刻出来！如果你知道你在寻找什么，并且知道那段数据在你感兴趣的文件格式中是如何存储的，那就不要雕刻！只需适应目标格式并搜索即可！那样会快得多。

```bash
#!/bin/bash
# Simple script to generate a vmdk
# Usage $0 <image>
# Copyright @security.com

if [ $# -ne 1 ]; then
  echo "Usage: $0 <image>"
  exit 1
fi

FILENAME=$1
LOOPDEVICE=""
SESEORS=""
CYLINDERS=""
# scan for first loop device
for i in `seq 0 9`
do
  losetup /dev/loop$i 2>/dev/null
  if [ $? -eq 0 ]; then
    LOOPDEVICE=/dev/loop$i
    break
  fi
done

if [ "$LOOPDEVICE" = "" ]; then
  echo "FATAL: no loop devices available!"
  exit 1
fi

# read geometry from fdisk
echo "Scanning..."
FDISKOUTPUT=$(fdisk -l $LOOPDEVICE | grep "Disk /")
TOTALSECTORS=$(echo "$FDISKOUTPUT" | awk '{print $2}')
TRACKSEORS=$(echo "$FDISKOUTPUT" | awk '{print $3}')
CYLINDERS=$(echo "$FDISKOUTPUT" | awk '{print $4}')
HEADS=$(echo "$FDISKOUTPUT" | awk '{print $5}')

# building the vmdk
echo "Writing $FILENAME.vmdk..."
cat << VMDK_EOF > $FILENAME
# DiskDescriptorFile
version=1
CID=7680558
parentCID=ffffff
createType="monolithicFlat"
# Extent description
RW $TOTALSECTORS FLAT "$FILENAME" 0
# The Disk Data Base
#DDB
dbb.adapterType = "ide"
db.geometry.sectors = "$TOTALSECTORS"
db.geometry.heads = "$HEADS"
db.geometry.cylinders = "$CYLINDERS"
dbb.virtualHWVersion = "4"
dbb.toolsVersion = "0"
VMDK_EOF
echo "Done!"
```

虚拟机是检查受损系统、测试新工具或在没有任何风险的情况下检查网络数据的完美环境。

| 检查清单 | 描述 |
| :--- | :--- |
| 拷贝 镜像并构建 vmdk 磁盘。 | 将 dd 镜像转换为 vmdk 文件。（你只需要构建一个小的文件）。 |
| 构建虚拟机。 | 使用新的 vmdk 创建虚拟机。 |
| 启动虚拟机并在受控环境中进行检查。 | 将虚拟机作为沙箱。你可以拍摄快照，使用主机作为防火墙限制网络访问，将 IDS 机器连接到虚拟网络等。虚拟机是测试受损主机和隐藏网络流量的好方法。 |

# 事后分析 (案例 4)

当你检查受损的网络时，可能需要检查所有可能的日志数据，仅仅是为了发现一条异常记录、关联来自不同源的日志、检查可疑活动等。

| 检查清单 | 描述 |
| :--- | :--- |
| 检查镜像分区表。 | 使用回环设备：`losetup /dev/[firstloopdevice] [image_file]` |

# 附录 B：Linux 取证与数据恢复

| 检查清单 | 描述 |
|--- | --- |
| 使用 fdisk, sfdisk 或 parted 查看分区表结构。 | 记得检查镜像以查看在扇区的结果。 |
| 以只读模式挂载镜像。 | `Mount -o ro,loop,nodev,user,noexec,notime,of,fset=[first_partition_cylinder*512] [image.file][mount_point]` |

## 处理电子证据
