# TABLE 11.1

# Tape Device Types

| Media Type | Capacity |
|---|---|
| 1/2-inch reel tape | 140MB (6250 BPI) |
| 1/4-inch cartridge tape (QIC) | 8GB |
| 8mm cartridge tape | 40–70GB |
| 4mm DAT cartridge tape (DDs-DDS4) | 1–40GB |
| DLT 1/2-inch cartridge tape (DLT2000-DLT7000) | 20–80GB |

To achieve higher capacity, one or more of these tape drives are combined into cabinets, called tape libraries or tape silos, capable of storing several terabytes of data spread across tens or even hundreds of tapes. Operating with robotic arms, tapes are located, retrieved, and loaded into a tape drive automatically to eliminate human intervention.

# Solaris Backup and Restoration Utilities

Solaris provides the utilities listed in Table 11.2. The backup utilities can be used to copy data from disk to removable media, and restore it.

# TABLE 11.2

# Backup Utilities

| Utility | Description |
|---|---|
| tar | Archives data to another directory, system, or medium. |
| dd | Copies data quickly. |
| cpio | Copies data from one location to another. |
| pax | Copies files and directory subtrees to a single tape. This utility provides better portability than tar or cpio, so it can be used to transport files to other types of UNIX systems. |
| ufsdump | Backs up all files in a file system. |
| ufsrestore | Restores some or all of the files archived with the ufsdump command. |