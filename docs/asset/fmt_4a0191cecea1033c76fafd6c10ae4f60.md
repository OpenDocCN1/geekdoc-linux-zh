
```python
if self.totalBlocks % self.blocksPerGroup != 0:
    bg += 1
return bg

def groupDescriptorSize(self):
    if '64-bit' in self.incompatibleFeaturesList:
        return 64
    else:
        return 32

def printState(self):
    # 0001/0002/0004 = 清洁卸载/错误/孤正在恢复
    retVal = "Unknown"
    if self.state == 1:
        retVal = "Cleanly unmounted"
    elif self.state == 2:
        retVal = "Errors detected"
    elif self.state == 4:
        retVal = "Orphans being recovered"
    return retVal

def printErrorBehavior(self):
    # 当错误 1/2/3 继续/只读/内核恐
    retVal = "Unknown"
    if self.errors == 1:
        retVal = "Continue"
    elif self.errors == 2:
        retVal = "Remount read-only"
    elif self.errors == 3:
        retVal = "Kernel panic"
    return retVal

def printCreator(self):
    # 0/1/2/3/4 Linux/Hurd/Masix/FreeBSD/Lites
    retVal = "Unknown"
    if self.creatorOs == 0:
        retVal = "Linux"
    elif self.creatorOs == 1:
        retVal = "Hurd"
    elif self.creatorOs == 2:
        retVal = "Masix"
    elif self.creatorOs == 3:
        retVal = "FreeBSD"
    elif self.creatorOs == 4:
        retVal = "Lites"
    return retVal

def printHashAlgorithm(self):
    # 0/1/2/3/4/5 legacy/half MD4/tea/u-legacy/u-half MD4/u-Tea
    retVal = "Unknown"
    if self.hashVersion == 0:
        retVal = "Legacy"
    elif self.hashVersion == 1:
        retVal = "Half MD4"
    elif self.hashVersion == 2:
        retVal = "Tea32sion"
    elif self.hashVersion == 3:
        retVal = "Unsigned Legacy"
    elif self.hashVersion == 4:
        retVal = "Unsigned Half MD4"
    elif self.hashVersion == 5:
        retVal = "Unsigned Tea"
    return retVal

def printEncryptionAlgorithms(self):
    enclList = []
    for v in self.encryptionAlgorithms:
        if v == 1:
            enclList.append('256-bit AES in XTS mode')
        elif v == 2:
            enclList.append('256-bit AES in GCM mode')
        elif v == 3:
            enclList.append('256-bit AES in CBC mode')
        elif v == 0:
            pass
        else:
            enclList.append('Unknown')
    return enclList

def pprint(self):
    for k, v in sorted(self._dict__.items()):
        if k == 'mountTime' or k == 'writeTime' or \
           k == 'journal' or k == 'mkfs' or \
           k == 'firstError' or k == 'lastError':
            print(k, v)
        elif k == 'state':
            print(k+":", self.printState())
        elif k == 'errors':
            print(k+":", self.printErrorBehavior())
        elif k == 'uuid' or k == 'journal':
            print(k+":", self.printCreator())
        elif k == 'creator':
            print(k+":", self.printHashAlgorithm())
        elif k == 'hashVersion':
            print(k+":", self.printEncryptionAlgorithms())
        elif k == 'encryptionAlgorithms':
            print(k+":", self.blockGroups())

def groupStartBlock(self, bgNo):
    return self.blocksPerGroup * bgNo

def groupEndBlock(self, bgNo):
    return self.blocksPerGroup * (bgNo + 1)

def groupStartInode(self, bgNo):
    return self.inodesPerGroup * bgNo

def groupEndInode(self, bgNo):
    return self.inodesPerGroup * (bgNo + 1)

def groupFromBlock(self, blockNo):
    return blockNo / self.blocksPerGroup

def groupIndexFromBlock(self, blockNo):
    return (blockNo - 1) % self.blocksPerGroup

def groupFromInode(self, inodeNo):
    return (inodeNo - 1) % self.inodesPerGroup

def groupHasSuperblock(self, bgNo):
    if bgNo == 0:
        return True
    return False

class GroupDescriptor():
    def __init__(self, data, wide=False):
        self.wide = wide
        # 块位
        self.blockBitmapLo = getU32(data)
        # inode 位图
        self.inodeBitmapLo = getU32(data, 4)
        # inode 表块
        self.inodeTableLo = getU32(data, 8)
        # 空闲块计数
        self.freeBlocksCount = getU16(data, 0xc)
        # 空闲 inode 计数
        self.freeInodesCount = getU16(data, 0xe)
```
