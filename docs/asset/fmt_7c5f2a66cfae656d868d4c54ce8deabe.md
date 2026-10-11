
```python
if not os.path.isfile(sys.argv[1]):
    print("File " + sys.argv[1] + " cannot be opened for reading")
    exit(1)

emd = ExtMetadata(sys.argv[1], sys.argv[2])
emd.prettyPrint()

if __name__ == "__main__":
    main()
```

```python
def groupIndexFromBlock(self, blockNo):
    return blockNo % self.blocksPerGroup

def groupFromInode(self, inode):
    return (inode - 1) / self.inodesPerGroup

def groupIndexFromInode(self, inode):
    return (inode - 1) % self.inodesPerGroup
```

### `Superblock` 类的 `groupHasSuperblock`

`Superblock` 类最后一个添加的函数是 `groupHasSuperblock`。如果你将块组编号传递给此函数，它将告诉你（好吧，不是字面上的你，但它会返回一个值）根据正在使用的特性，该块是否包含超级。该函数的代码如下：

```python
def groupHasSuperblock(self, bgNo):
    # 块组 0 总是有一个超级
    if bgNo == 0:
        return True

    if 'Meta Block Groups' in self.incompatibleFeaturesList and \
        bgNo >= self.firstMetaBlockGroup:
            # 块组在每个元组的第一个、
            # 第二个和最后一个中拥有 sb 和 gdt
            # 块组大小为 blockSize/32
            # 只有部分文件使用此特性
            mbgSize = self.blockSize / 32
            retVal = (bgNo % mbgSize == 0) or \
                ((bgNo + 1) % mbgSize == 0) or \
                (bgNo - 1) % mbgSize == 0)

    elif 'Sparse Super' in self.compatibleFeaturesList:
        # self.backupBlockGroups 中有两个备份超级
        if bgNo == self.backupBlockGroups[0] or \
            bgNo == self.backupBlockGroups[1]:
            retVal = True

    elif 'Sparse Super' in self.readonlyCompatibleFeaturesList:
        # 备份在 1、3 的幂次和 5 的幂中
        retVal = (bgNo == 1) or \
            (bgNo == pow(3, round(bgNo) / log(3))) or \
            (bgNo == pow(5, round(bgNo) / log(5))) or \
            (bgNo == pow(7, round(bgNo) / log(7)))

    if retVal:
        return retVal
    else:
        # 如果我们运行到这里，必须是默认情况
        # 每个 bg 都有 sb 和 gdt
        retVal = True
        return retVal
```

该函数主要是一个大的 `if/elif/else` 块。它首先检查块组是否为 `0`。如果是，它会立即返回 `True`，因为第一个组中始终有一个超级。

接下来，我们检查 `Meta Block Groups`（元块组）特性。记住，该特性将文件系统分成多个元组。元组就像小文件系统，其组描述符仅与元组内部的块组相关。当此特性启用时，元组内的第一个、第二个和最后一个块组中有一个超级块和一个组描述符表。元组的大小始终为 `blocksize / 32`。此外，超级组可能只适用于磁盘的一部分，因此需要进行检查以确保我们处于存在元组的区域。

接下，我们检查 `Sparse Super 2`（稀疏超级 2）特性。该特性在超级中列出的两个组中存储备份超级。下一个检查是 `Sparse Super` 特性。如果正在使用此特性，备份超级位于组 `1` 且是 `3`、`5` 或 `7` 的幂次。这就是之前对数函数起作用的地方。对于 `$x$` 的任何偶次幂，`$x^{\text{rounded}(\log(n))}$` 应该等于 `$n$`。

### `GroupDescriptor` 与 `ExtendedDescriptor`

`GroupDescriptor` 类保持不变。我们添加了一个新类 `ExtendedDescriptor`，它将我们的超级块信息与组描述符相结合，以完整描述块组。这个新类在通用 `GroupDescriptor` 类发现的内容的基础上增加了布局信息。有些人可能会质疑，为什么我选择不让 `ExtendedDescriptor` 类继承（或扩展）`GroupDescriptor` 类。主要原因是 `GroupDescriptor` 类在存储原始数据结构上较小，而 `ExtendedDescriptor` 包含了从原始值派生的意义成员。该类的代码如下：

```python
class ExtendedDescriptor():
    def __init__(self, bgd, sb, bgNo):
        self.blockGroup = bgNo
        self.startBlock = sb.groupStartBlock(bgNo)
        self.endBlock = sb.groupEndBlock(bgNo)
        self.startInode = sb.groupStartInode(bgNo)
        self.endInode = sb.groupEndInode(bgNo)
        self.flags = bgd.printList()
        self.freeInodes = bgd.freeInodesCount
        if bgd.wide:
            self.freeInodes += bgd.freeInodesHi * pow(2, 16)
        self.freeBlocks = bgd.freeBlocksCount
        if bgd.wide:
            self.freeBlocks += bgd.freeBlocksCount * pow(2, 16)
        self.directories = bgd.usedDirsCount
        if bgd.wide:
            self.directories += bgd.usedDirsHi * pow(2, 16)
        self.checksum = bgd.blockBitmapCsumLo
        if bgd.wide:
            self.checksum += bgd.blockBitmapCsumHi * pow(2, 16)
            self.inodeBitmapChecksum = bgd.inodeBitmapCsumLo
        if bgd.wide:
            self.inodeBitmapChecksum += bgd.inodeBitmapHi * pow(2, 16)
        # 现在确定布局并存储在列表中（嵌套列表）
        self.layout = []
        self.nonDataBlocks = 0
        # 为灵活块组进行调整
        fbgAdj = 1
        if 'Flexible Block Groups' in sb.incompatibleFeaturesList:
            # 仅影响灵活组中的第一个组
            if bgNo % sb.groupsPerFlex == 0:
                fbgAdj = sb.groupsPerFlex
            if sb.groupHasSuperblock(bgNo):
```
