
这定义了一个建议的 `Disk` 数据结构。逻辑扇区从 0 开始编号，尽管磁道上的单个扇区通常从 1 开始编号。磁道 T、头部 H、扇区 S 逻辑 L 位于：

```
L = S - 1 + T * (heads * sectorsPerTrack) + H * sectorsPerTrack
```

你不需要执行从逻辑扇区到磁道/头部/扇区的坐标转换，因为操作系统会为你完成。

## 实验 5.1 软盘驱动程序

第一个要实现的基于对物理磁盘直接 I/O 磁盘抽象的函数：

`Disk physicalDisk(char driveLetter);`

要实现此函数，你必须使用主机操作系统的内核 `open()` 函数，并将其应用于软盘。确保还执行以下操作：

- 将驱动器号映射为大写字符。
- 如果你使用 DOS，转义 C 字符串字面量中的所有反斜杠。

在 Windows 中，对 `CreateFile()` 调用中的 `dwCreationDistribution` 参数使用 `OPENEXIST`。对 `dwFlagsAndAttributes` 参数使用 `FILE_FLAG_NO_BUFFERING` 和 `FILE_FLAG_RANDOM_ACCESS`。在 `fdwShareMode` 参数中，你必须设置 `GENERIC_READ`、`GENERIC_WRITE`、`FILE_SHARE_READ` 和 `FILE_SHARE_WRITE` 标志。一旦打开磁盘，你就可以 `DeviceIoControl()` 获取几何结构。

以下显示用于设计的头文件内容：

> * 此接口衍生自 Norman Ramsey 为 1996 年普渡大学 CSCi 413 课程设计的

```c
#ifndef DISKMODULE_H

#define DISKMODULE_H

#define BOOT -1

#define FAT1 -2

#define FAT2 -3

#define BOOT_SECTOR 0

#define FAT1_SECTOR 1

#define FAT2_SECTOR 10

#define ROOT_SECTOR 19

#include <windows.h>

#include <winioctl.h> // DISK_GEOMETRY

struct geometry {
    unsigned bytesPerSector; // 每个扇区的字节数
    unsigned sectorsPerTrack; // 每个磁道的扇区数
    unsigned heads; // 每个柱面上的磁道数
    unsigned cylinders; // 磁盘上的柱面数
};

typedef struct disk *Disk;

struct disk {
    HANDLE floppyDisk;
    DISK_GEOMETRY geometry;
}

/* Disk 上的函数原型 */

// 磁盘的抽象
Disk physicalDisk(char driveLetter);
void sectorDump(Disk, int sectorNumber);
BOOL DeviceIoControl(Disk, unsigned *);

#endif // DISKMODULE_H
```

## 解决方案

你可以按照以下顺序考虑你的解决方案：

1. 实现 `physicalDisk()`。
2. 编写一个可以任意转储扇区的 `sectorRead()` 实现。
3. 使用你的 `sectorDump()`。

以下是 `main()` 的骨架：

```c
#include <stdio.h>
// 上述数据结构

int main() {
    Disk theDisk;
    int firstSector, lastSector, i;
    firstSector = ...; // 你想要显示的起始扇区
    lastSector = ...; // 你想要显示的结束扇区
    theDisk = physicalDisk(...);
    // 某些扇区
    sectorDump(theDisk, BOOT);
    sectorDump(theDisk, FAT1);
    sectorDump(theDisk, FAT2);
    if(firstSector >= 0) {
        for(i = firstSector; i <= lastSector; i++) {
            sectorDump(theDisk, i);
        }
    }
    return 0;
}
```
