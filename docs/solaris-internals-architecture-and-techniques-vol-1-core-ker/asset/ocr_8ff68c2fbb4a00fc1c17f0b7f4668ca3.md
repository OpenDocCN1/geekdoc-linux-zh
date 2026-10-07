626

Kernel Virtual Address Maps

| | |
|---|---|
| 0xFFFFFFFF | Invalid |
| 0xFFFF0000 | Monitor |
| 0xFFFD0000 | Kernel Heap
segkmem (251 Mbytes) |
| 0xF0200000 | File System Cache segmap (32 Mbytes) |
| 0xF0080000 | Pageable Kernel Mem. segkp |
| 0xEE080000 | sun4d HAT Structures |
| | Kernel Data Segment |
| | Kernel Text Segment |
| 0xE0040000 | Trap Table (4 Kbytes) |
| 0xE0000000 | Process Address Space |
| 0x0 | |

Figure B.4 Solaris 7 sun4d 32-Bit Kernel Address Space