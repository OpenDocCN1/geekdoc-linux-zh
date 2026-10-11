
`root@i7laptop:~/Videos# file *.mp3`

HDV 0081.mp3: MPEG ADTS, layer III, v1, 128 kbps, 48 kHz, JointStereo

HDV 0083.mp3: MPEG ADTS, layer III, v1, 128 kbps, 48 kHz, JointStereo

HDV 0084.mp3: MPEG ADTS, layer III, v1, 128 kbps, 48 kHz, JointStereo

HDV 0085.mp3: MPEG ADTS, layer III, v1, 128 kbps, 48 kHz, JointStereo

the marines hymn.mp3: Audio file with ID3 version 2.3.0, contains: MPEG ADTS, layer III, v1, 128 kbps, 44.1 kHz, JointStereo

`root@i7laptop:~/Videos#`

# 图 7.9

在 `i7laptop:~/Videos` 上针对普通文件运行 `file` 命令的输出。

```
root@i7laptop:~/Videos# file -sl /dev/sd*
```

`/dev/sda1`: Linux partition, GPT table, LFS root, size 50 GiB, type Linux ext4 data

`/dev/sda2`: Linux partition, GPT table, LFS swap, size 8.0 GiB, type Linux swap-data

`/dev/sda3`: Linux partition, GPT table, LFS home, size 200 GiB, type Linux ext4 data

`/dev/sda4`: Linux partition, GPT table, LFS backup, size 100 GiB, type Linux ext4 data

`/dev/sda5`: Linux partition, GPT table, LFS media, size 500 GiB, type Linux ext4 data

`/dev/sda6`: Linux partition, GPT table, LFS games, size 300 GiB, type Linux ext4 data

`/dev/sda7`: Linux partition, GPT table, LFS projects, size 150 GiB, type Linux ext4 data

`/dev/sda8`: Linux partition, GPT table, LFS work, size 100 GiB, type Linux ext4 data

`/dev/sda9`: Linux partition, GPT table, LFS test, size 50 GiB, type Linux ext4 data

# 图 7.10

从图 7.10 可以看出 Linux 具有日志功能、使用区（extents）并支持大文件。这些功能将在本章节后面进行详细描述。

元块组（Meta Block Group）将文件系统分为许多元块组，其大小使得组描述符可以存储在单个块中。这使得大于 256 TB 的文件系统变得可用。

区范围（Extents）功能允许更高效地处理大文件。区范围与 NTFS 的数据运行（data runs）类似，它们都允许更高效地存储和访问大文件。本章稍后部分将详细讨论区范围。

64位功能将最大块数从 `$2^{32}$` 增加到 `$2^{64}$`。这并不是一个常见的功能，因为 32 位模式支持多达 256 PB 的文件系统。它在需要较小块大小的场景中更为常见，例如存储大量小文件的服务器。

多重挂载保护（Multiple Mount Protection）功能用于检测是否有多个操作系统或进程正在使用某个文件系统。当启用此功能时，任何尝试挂载已挂载文件系统的操作将失败。作为双重检查，系统会定期重新检查挂载状态（序列号），如果操作系统检测到另一个系统挂载了该文件系统，则文件系统将保持为只读状态。

与区范围类似，灵活块（flexible blocks）被用于更高效地处理大文件。当启用灵活块组（Flex Block Group）功能时，相邻块组中的某些项会被移动，以便在某些组中留更多数据块，从而大文件更有机会连续存储。此功能通常与区范围结合使用。

扩展属性（Extended attributes）在上一节中讨论过。如果支持扩展属性，它们可能存储在节点（inodes）或数据块中。如果设置了扩展属性内（Extended Attribute In）标志，则操作系统必须支持在扩展属性存在的任何地方从节点中读取扩展属性。

我们已经看到了几项允许更高效地处理大文件的功能。目录数据（Directory Data）功能是针对小文件的优化。当启用此功能时，小文件可以完全存储在它们的目录条目中。较大的文件可能被划分在目录条目和数据块之间。由于前几个字节包含文件签名，将文件的开头放在目录条目中可以加快操作，因为不再需要读取数据块来确定文件类型。内联数据（Inline Data）功能与之类似，但数据存储在节点中而不是目录条目中。

剩余的不兼容功能分别是组元数据校验和（Group Meta Checksum）、大目录（Large Directory）和加密（Encrypt），它们分别表示元数据的校验和存储在块组中、存在大于 2 GB 或使用 3 级哈希树的目录，以及节点已加密。这些功能均不常见。

对于所有不兼容的功能，我们最感兴趣的是那些影响文件系统布局的项。有三项此类功能：灵活块（Flexible Block）、元块（Meta Block）和 64 位模式（64-bit Mode）。灵活块组将多个块组组合在一个灵活组中。灵活组的大小通常是 2 的幂。数据和节点位图仅存在于灵活组中的第一个块组中。这使得某些组完全由数据块组成，从而大文件可以在不产生碎片的情况下进行存储。

当使用元块组时，文件系统被划分为几个称为元块组的逻辑分区。组描述符只位于每个元块组的第一个、第二个和最后一个块组中。

使用 64 位模式不会直接影响文件系统布局。相反，其影响是间接的，因为当在使用 64 位模式时，某些结构的大小会增加。

## 只读兼容特性

只读兼容特性要求能够修改数据，但不需要能够正确读取数据。显然，你不应该针对文件系统运行其中一个或多个此类特性的 `fsck`。只读兼容特性总结在表 7.4 中。

### 表 7.4. 只读兼容特性。

| 位 | 名称 | 描述 |
|---|---|---|
| 0x1 | Sparse Super | 稀疏超级块（仅在 BG 0 或 3, 5, 7 的幂次中） |
| 0x2 | Large File | 文件系统中存在大于 2GB 的文件 |
| 0x4 | Btree Dir | 目录中使用了 B 树（不常见） |
| 0x8 | Huge File | 文件大小以逻辑块表示，而非扇区 |
| 0x10 | Gdt Csum | 组描述符表具有校验和 |
| 0x20 | Dir Nlink | 子目录条目数不限于 32k 个 |
| 0x40 | Extra Isize | 表示文件系统中存在大节点 |
| 0x80 | HasSnapshot | 文件系统具有快照 |
| 0x100 | Quota | 文件系统正在使用磁盘配额 |
| 0x200 | BigAlloc | 区范围在多块簇中进行跟踪 |
| 0x400 | Metadata Csum | 元数据项使用了校验和 |
| 0x800 | Replica | 文件系统支持副本 |
| 0x1000 | ReadOnly | 应该仅挂载为只读 |

当使用超级块功能时，超级块仅位于块组 0 或位为 3, 5, 7 的幂次的的块组中。如果文件系统中至少有一个大于 2 GB 的文件，则 Large File 特性标志将被设置。Huge File 特性标志表示至少存在一个大文件。大文件的大小以簇指定（大小存储在超级块中），而非数据块。

Btree 目录功能允许大目录存储在二叉树中。这并不常见。另一个与大目录相关的特性是目录链接数（Directory Nlink）。当设置 Nlink 标志时，子目录的条目数不限于 32k 个。

遍历了大部分代码，但并非所有代码。关于格式的说明：原本位于行尾的许多注释已移动到行上方，以便使书中的代码更易读。

```python
#!/usr/bin/python

#
# extfs.py
#
# 这是一个简单的 Python 脚本，用于
# 从镜像文件内部的 ext2/3/4 文件系统中
# 获取元数据
#
### 为 PentesterAcademy 开发
# 作者 Phil Polstra 博士 (@ppolstra)
import sys
import os.path
import subprocess
import struct
import time
# 这些是为了方便转换的简单函数
```
