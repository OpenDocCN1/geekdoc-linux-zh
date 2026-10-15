
```python
def getu32(data, offset=0):
    return struct.unpack('<L', data[offset:offset+4])[0]

def getu16(data, offset=0):
    return struct.unpack('<H', data[offset:offset+2])[0]

def getu8(data, offset=0):
    return struct.unpack('B', data[offset:offset+1])[0]

def getu64(data, offset=0):
    return struct.unpack('<Q', data[offset:offset+8])[0]

# 此函数不解包字符串，因为
# 它不是真正的数字而是一个 UUID
def getu128(data, offset=0):
    return data[offset:offset+16]

def printUuid(data):
    retStr = \
    format(struct.unpack('<Q', data[8:16])[0], 'X').zfill(16) + \
    format(struct.unpack('<Q', data[0:8])[0], 'X').zfill(16)
    return retStr

def getCompatibleFeaturesList(u32):
    retList = []
    if u32 & 0x1:
        retList.append('Directory Preallocate')
    if u32 & 0x2:
        retList.append('Immutable Inodes')
    if u32 & 0x4:
        retList.append('Has Journal')
    if u32 & 0x8:
        retList.append('Extended Attributes')
    if u32 & 0x10:
        retList.append('Resize Node')
    if u32 & 0x20:
        retList.append('Directory Index')
    if u32 & 0x40:
        retList.append('Lazy Block Groups')
    if u32 & 0x80:
        retList.append('Exclude Inode')
    if u32 & 0x100:
        retList.append('Exclude Bitmap')
    if u32 & 0x200:
        retList.append('Sparse Super 2')
    return retList

def getIncompatibleFeaturesList(u32):
    retList = []
    if u32 & 0x1:
        retList.append('Compression')
    if u32 & 0x2:
        retList.append('Filetype')
    if u32 & 0x4:
        retList.append('Recover')
    if u32 & 0x8:
        retList.append('Journal Device')
    if u32 & 0x10:
        retList.append('Meta Block Groups')
    if u32 & 0x40:
        retList.append('Extents')
    if u32 & 0x80:
        retList.append('64-bit')
    if u32 & 0x100:
        retList.append('Multiple Mount Protection')
    if u32 & 0x200:
        retList.append('Flexible Block Groups')
    if u32 & 0x400:
        retList.append('Extended Attributes in Inodes')
    if u32 & 0x1000:
        retList.append('Directory Data')
    if u32 & 0x2000:
        retList.append('Block Group Metadata Checksum')
    if u32 & 0x4000:
        retList.append('Large Directory')
    if u32 & 0x8000:
        retList.append('Inline Data')
    if u32 & 0x10000:
        retList.append('Encrypted Inodes')
    return retList

def getReadOnlyCompatibleFeaturesList(u32):
    retList = []
    if u32 & 0x1:
        retList.append('Sparse Super')
    if u32 & 0x2:
        retList.append('Large File')
    if u32 & 0x4:
        retList.append('Btree Directory')
    if u32 & 0x8:
        retList.append('Huge File')
    if u32 & 0x10:
        retList.append('Group Descriptor Table Checksum')
    if u32 & 0x20:
        retList.append('Directory Nlink')
    if u32 & 0x40:
        retList.append('Extra Isize')
    if u32 & 0x80:
        retList.append('Has Snapshot')
    if u32 & 0x100:
        retList.append('Quota')
    if u32 & 0x200:
        retList.append('Big Alloc')
    if u32 & 0x400:
        retList.append('Metadata Checksum')
    if u32 & 0x800:
        retList.append('Replica')
    if u32 & 0x1000:
        retList.append('Read-only')
    return retList

# 此 Superblock 将解析 superblock中的数据
class Superblock:
    def __init__(self, data):
        self.totalInodes = getu32(data)
        self.totalBlocks = getu32(data, 4)
        self.restrictedBlocks = getu32(data, 8)
        self.freeBlocks = getu32(data, 0xc)
        self.freeInodes = getu32(data, 0x10)
        # 通常块大小为 <4k
        self.firstDataBlock = getu32(data, 0x14)
        # 块大小为 1024 * 2^(字段的值)
        self.blockSize = getu32(data, 0x18)
        # 如果启用 bigalloc
        self.clusterSize = getu32(data, 0xc)
        self.blocksPerGroup = getu32(data, 0x20)
        # 如果启用 bigalloc
        self.clustersPerGroup = getu32(data, 0x24)
        self.inodesPerGroup = getu32(data, 0x28)
```
