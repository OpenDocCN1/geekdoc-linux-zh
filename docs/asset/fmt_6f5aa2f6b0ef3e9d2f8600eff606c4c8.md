
# mount-image-gpt.py

```python
#!/usr/bin/python

### mount-image-gpt.py

# 这是一个简单的 Python 脚本，将
# 尝试从镜像文件中挂载分区。
### 此脚本仅用于 GUID 分区。
### 镜像以只读方式挂载。

### 由 Dr. Phil Polstra (@ppolstra) 开发
### 为 PentesterAcademy.com
import sys
import os.path
import subprocess
import struct
### 支持的分区类型的 GUID
supportedParts = ["E0DB00A2-B9E5-4433-87C0-68B7269C7C9", "37AFC090-EF7D-4E96-1C3D-27AE055B1744", "0FC63DAF-8483-4772-8E79-36D98477DE4E", "8DA63339-0007-60C0-C436-083AC823090A",
"AC378E1-2EB4-4F13-BB44-0E14E2AF915", "4479540-F297-B12-9AF7-D13D5F0458A", "6F8BC3E-E8CD-4D1-96E7-ECBF948B709", "B21B0A45-1DF0-41C3-AF44-46F280D3FAE", "3B8F425-2E50-4F3B-907-1A25C47698E5", "6D06379-F507-44C2-A23C-238F2A309712B", "516E7CB84-66CF-11D6-8FF8-00022D09712B", "83D6B9D-7F41-11D6-CE0B-0156B84F0F", "516E7CB5-B6CF-11D6-8FF8-00022D09712B", "85D5E45A-237C-11E1-B4B3-E89A8F7CA37", "516E7CB4-66CF-11D6-8FF8-00022D09712B", "824CC70-36A8-11E3-89A0-52519AD3F61", "55465300-0000-11AA-A11-00306543ACE3", "516E7CB5-66CF-11D6-8FF8-00022D09712B", "49F8D5A-B10E-11DC-B99B-0019D179684", "49F4BD82-B10E-11DC-B99B-0019D179684", "2DB519C4-B10F-11DC-B99B-0019D179684", "2DB519EC-B10E-11DC-B99B-0019D179684", "49F4D8AA-B10E-11DC-B99B-0019D179684", "42F6GF74-0000-11AA-A11-00306543ACE3", "48465300-0000-11AA-A11-00306543ACE3", "52414944-0000-11AA-A11-00306543ACE3", "52414944-0000-11AA-A11-00306543ACE3", "4C612625-0000-11AA-A11-00306543ACE3", "6A82CB45-10D2-11D2-99A6-08002073661", "6A85CF4D-10D2-11D2-99A6-08002073661", "6A988CC3-10D2-11D2-99A6-08002073661", "6A8B642B-10D2-11D2-99A6-08002073661", "6A8EF2E9-10D2-11D2-99A6-08002073661, "69A0BA39-10D2-11D2-99A6-08002073661, "6A9283A5-10D2-11D2-99A6-08002073661, "758941C3-AEB-11D3-B7C1-7B0300, "E2A1E728-32E3-11D6-A682-7B0300, "BC13C2FF-59E6-4262-A352-B275D6F172, "42465331-BA33-10F1-80A2-486196752, "33AA1E2A-400F-11DB-9590-00022911DB8, "9198EFF-31C0-11DB-B87F-00022911DB8, "9D275380-40AD-11DB-BF97-00022911DB8, "A1D98B0F-0F5C-4D3B-A006-743F0F8491E

### 打印 GUID 的简单辅助函数
### 注意它们都是小端/大端格式
def printGuid(packedString):
    if len(packedString) == 16:
        outstr = format(struct.unpack('<L',
            packedString[0:4])[0], 'X').zfill(8) + "-" +
            format(struct.unpack('<H',
            packedString[4:6])[0], 'X').zfill(4) + "-" +
            format(struct.unpack('<H',
            packedString[6:8])[0], 'X').zfill(4) + "-" +
            format(struct.unpack('<Q',
            packedString[8:10])[0], 'X').zfill(4) + "-" +
            format(struct.unpack('>Q',
            "\x00\x00" + packedString[10:16])[0], 'X').zfill(12)
    else:
        outstr = "<invalid"
    return outstr

### GptRecord 类

### 解析 GUID 分区条目
# 用法: rec = GptRecord(recs, partno)
# recs 是包含所有 128 个条目的字符串
### partno 是感兴趣的分区号 (0-127)
### rec.printPart() 打印分区信息

class GptRecord:

    def __init__(self, recs, partno):

        self.partno = partno

        offset = partno * 128

        self.empty = False

        # 构建分区类型字符串

        self.partType = printGuid(recs[offset:offset+16])

        if self.partType == "00000000-0000-0000-000000000000":

            self.empty = True

        self.partGuid = printGuid(recs[offset+16:offset+32])

        self.firstLBA = struct.unpack('<Q',

            recs[offset+32:offset+40])[0]

        self.lastLBA = struct.unpack('<Q',

            recs[offset+40:offset+48])[0]

        self.attr = struct.unpack('<Q',

            recs[offset+48:offset+56]) [0]

        nameIndex = recs[offset+56:offset+128].find('\x00\x00')

        if nameIndex != -1:

            self.partName = \
            recs[offset+56:offset+nameIndex].encode('utf-8')

        else:

            self.partName = \
            recs[offset+56:offset+128].encode('utf-8')

    def printPart(self):

        if not self.empty:

            outstr = str(self.partno) + ":" + self.partType +
                ":" + self.partGuid + ":" + str(self.firstLBA) +
                ":" + str(self.lastLBA) + ":" +
                str(self.attr) + ":" + self.partName

        print(outstr)
```
