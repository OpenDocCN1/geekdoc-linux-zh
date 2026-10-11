Press any key.

When you press a key, a root partition screen similar to the following appears. (Note that, if the computer has more than one hard drive, you’ll be asked to select which one you want to partition.)

# **Figure D–2 FIPS Root Partition Screen**

Partition table:

| Part. | bootable | Start Head Cyl. Sector | System | End Head Cyl. Sector | Start Sector | Number of Sectors | MB |
|---|---|---|---|---|---|---|---|
| 1 | yes | 0 148 1 | 83h | 15 295 63 | 149184 | 149184 | 72 |
| 2 | no | 0 0 1 | 06h | 15 139 63 | 63 | 141057 | 68 |
| 3 | no | 0 140 1 | 06h | 15 147 63 | 141120 | 8064 | 3 |
| 4 | no | 0 0 0 | 00h | 0 0 0 | 0 | 0 | 0 |

Checking root sector ... OK

Press any key.

When you press a key, details about the hard drive, such as the following, will appear.

# **Figure D–3 FIPS Boot Sector Screen**

```
Boot sector:
Bytes per sector: 512
Sectors per cluster: 8
Reserved sectors: 1
Number of FATs: 2
Number of root directory entries: 512
Number of sectors (short): 0
Media descriptor byte: f8h
Sectors per FAT: 145
Sectors per track: 63
Drive heads: 16
Hidden sectors: 63
Number of sectors (long): 141057
Physical drive number: 80h
Signature: 29h
```