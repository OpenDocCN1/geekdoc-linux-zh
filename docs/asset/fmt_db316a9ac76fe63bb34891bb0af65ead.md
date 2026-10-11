
```python
if u32 & 0x8000:
    retList.append('Inline Data') # 内联数据

if u32 & 0x10000:
    retList.append('Encrypted Inodes') # 加密 Inode

return retList

def getReadOnlyCompatibleFeaturesList(u32):
  retList = []

  if u32 & 0x1:
    retList.append('Sparse Super') # 稀疏超级块

  if u32 & 0x2:
    retList.append('Large File') # 大文件

  if u32 & 0x4:
    retList.append('Btree Directory') # Btree 目录

  if u32 & 0x8:
    retList.append('Huge File') # 巨大文件

  if u32 & 0x10:
    retList.append('Group Descriptor Table Checksum') # 组描述表校验和

  if u32 & 0x20:
    retList.append('Directory Nlink') # 目录链接数

  if u32 & 0x40:
    retList.append('Extra Isize') # 额外 Isize

  if u32 & 0x80:
    retList.append('Has Snapshot') # 带有快照

  if u32 & 0x100:
    retList.append('Quota') # 配额

  if u32 & 0x200:
    retList.append('Big Alloc') # 大内存分配

  if u32 & 0x400:
    retList.append('Metadata Checksum') # 元数据校验和

  if u32 & 0x800:
    retList.append('Replica') # 副本

  if u32 & 0x1000:
    retList.append('Read-only') # 只读

  return retList
```

此类将解析来自扩展 (`ext2`/`ext3`/`ext4`) Linux 文件系统的超级块中的数据。
截至 2015 年 7 月为最新状态。
用法：`sb.Superblock(data)`，其中
`data` 是一个至少 1024 字节的紧包字符串，
其前 1024 字节包含一个超级块。
`sb.prettyPrint()` 会打印超级块中的所有字段。

```python
class Superblock():
    def __init__(self, data):
        self.totalInodes = getU32(data) # 总 Inode 数
        self.totalBlocks = getU32(data, 4) # 总块数
        self.restrictedBlocks = getU32(data, 8) # 受限块数
        self.freeBlocks = getU32(data, 0xc) # 空闲块数
        self.freeInodes = getU32(data, 0x10) # 空闲 Inode 数
        # 除非块大小小于 4，否则正常
        self.firstDataBlock = getU32(data, 0x14)
        # 块大小 = 1024 * 2^(字段值)
        self.blockSize = pow(2, getU32(data, 0x18))
        # 仅在 bigalloc 特性下
        self.clusterSize = pow(2, getU32(data, 0x1c))
        self.blocksPerGroup = getU32(data, 0x20) # 每组块数
        # 仅在 bigalloc 特性下
        self.clustersPerGroup = getU32(data, 0x24) # 每组簇数
        self.inodesPerGroup = getU32(data, 0x28) # 每组 Inode 数
        self.mountTime = time.gtime(getU32(data, 0x2c)) # 挂载时间
        self.writeTime = time.gtime(getU32(data, 0x30)) # 写时间
        # 自上次 fsck 起
        self.mountCount = getU16(data, 0x34) # 挂载次数
        # 两次 fsck 之间
        self.maxMountCount = getU16(data, 0x36) # 最大挂载次数
        # 应为 0xef
        self.magic = getU16(data, 0x38) # 魔幻数
        # 0x01/0x02/0x04 = 干净卸载/错误/崩溃
        self.state = getU16(data, 0x3a) # 状态
        # 错误 1/2/3 继续只读
        self.errors = getU16(data, 0x3c) # 错误计数
        self.minorRevision = getU16(data, 0x3e) # 小版本
        # 上次 fsck
        self.lastCheck = time.gtime(getU32(data, 0x40)) # 最后检查时间
        # 检查间隔秒
        self.checkInterval = getU32(data, 0x44) # 检查间隔
        # 0/1/2/3/4 Linux/Hard/FreeBSD/Linux
        self.creatorOs = getU32(data, 0x48) # 创建操作系统
        # 0/1/v2 动态 inode 大
        self.revisionLevel = getU32(data, 0x4c) # 版本级别
        # 预留块的 UID
        self.defaultUid = getU16(data, 0x50) # 默认 UID
        # 预留块的 GID
        self.defaultGid = getU16(data, 0x52) # 默认 GID
        # 仅 Ext4 动态
        self.firstInode = getU32(data, 0x54) # 第一个 inode
        # inode 大字节字节
        self.inodeSize = getU16(data, 0x58)
        # 该超级块所在的块组
        self.blockGroupNumber = getU16(data, 0x5a) # 块组号
        # 兼容特性
        self.compatibleFeatures = getU32(data, 0x5c)
        self.compatibleFeaturesList = getCompatibleFeaturesList(self.compatibleFeatures)
        # 不兼容特性
        self.incompatibleFeatures = getU32(data, 0x60)
        self.incompatibleFeaturesList = getIncompatibleFeaturesList(self.incompatibleFeatures)
        # 只读兼容特性
        self.readOnlyCompatibleFeatures = getU32(data, 0x64)
        self.readOnlyCompatibleFeaturesList = getReadOnlyFeaturesList(self.readOnlyCompatibleFeatures)
        # 紧包字符串卷 UUID
        self.uuid = getU28(data, 0x68)
        # 卷名 - 可能为空
        self.volumeName = data[0x78:0x88].split("\x00")[0]
        # 最后挂载的目录
```
