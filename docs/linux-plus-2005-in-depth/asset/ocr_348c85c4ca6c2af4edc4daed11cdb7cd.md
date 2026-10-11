Notice from preceding output that the default type for new partitions created with fdisk is 83 (Linux); to change this, you can type the `t` key at the fdisk prompt. To change the /dev/hdc6 partition to type 82 (Linux swap), you can do the following at the fdisk prompt:

Command (m for help): **t**
Partition number (1-6): **6**
Hex code (type L to list codes): **L**

+   * 0 Empty
+   * 1 FAT12
+   * 2 XENIX root
+   * 3 XENIX usr
+   * 4 FAT16 <32M
+   * 5 Extended
+   * 6 FAT16
+   * 7 HPFS/NTFS
+   * 8 AIX
+   * 9 AIX bootable
+   * a OS/2 Boot Manag
+   * b W95 FAT32
+   * c W95 FAT32 (LBA)
+   * e W95 FAT16 (LBA)
+   * f W95 Ext'd (LBA)
+   * 10 OPUS
+   * 11 Hidden FAT12
+   * 12 Compaq diagnostic
+   * 14 Hidden FAT16 <32
+   * 16 Hidden FAT16
+   * 17 Hidden HPFS/NTF
+   * 18 AST SmartSleep
+   * 1b Hidden W95 FAT3

+   * 1c Hidden W95 FAT
+   * 1e Hidden W95 FAT
+   * 24 NEC DOS
+   * 39 Plan 9
+   * 40 Venix 80286
+   * 41 PPC PReP Boot
+   * 42 SFS
+   * 4d QNX4.x
+   * 4e QNX4.x 2nd pa
+   * 4f QNX4.x 3rd pa
+   * 50 OnTrack DM
+   * 51 OnTrack DM Aua
+   * 52 CP/M
+   * 53 Hidden DM6 Auu
+   * 54 OnTrackDM6
+   * 55 EZ-Drive
+   * 56 Golden Bow
+   * 5c Priam Edisk
+   * 61 SpeedStor
+   * 63 GNU HURD or Sy
+   * 64 Novell Netware
+   * 65 Novell Netware

+   * 70 DiskSecure Mult
+   * 75 PC/IX
+   * 80 Old Minix
+   * 81 Minix / old Li
+   * 82 Linux swap
+   * 83 Linux
+   * 84 OS/2 hidden C:
+   * 85 Linux extended
+   * 86 NTFS volume set
+   * 87 NTFS volume set
+   * 8e Linux LVM
+   * 93 Amoeba
+   * 94 Amoeba BBT
+   * 9f BSD/OS
+   * a0 IBM Thinkpad
+   * a5 FreeBSD
+   * a6 OpenBSD
+   * a7 NetXStep
+   * a8 Darwin UFS
+   * a9 NetBSD
+   * ab Darwin boot
+   * b7 BSDI fs
+   * b8 BSDI swap

+   * bb Boot Wizard hid
+   * be Solaris boot
+   * c1 DRDOS/sec (FAT
+   * c5 DRDOS/sec (FAT
+   * c6 DRDOS/sec (FAT
+   * c7 Syrrinx
+   * da Non-FS data
+   * db CP/M / CTOS / .
+   * df Dell Utility
+   * e0 BootIt
+   * e1 DOS access
+   * e3 DOS R/O
+   * e4 Dell SpeedStor
+   * eb BeOS fs
+   * ee EFI GPT
+   * ef EFI (FAT-12/16/
+   * f0 Linux /Par-RISC b
+   * f1 SpeedStor
+   * f4 SpeedStor
+   * f2 DOS secondary
+   * fd Linux raid auto
+   * fe LANstep
+   * ff BBT

Hex code (type L to list codes): **82**
Changed system type of partition 6 to 82 (Linux swap)

Command (m for help): **p**

Disk /dev/hdc: 20.4 GB, 20490559488 bytes
255 heads, 63 sectors/track, 2491 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes

| Device | Boot | Start | End | Blocks | Id | System |
| :--- | :---: | :---: | :---: | :---: | :---: | :--- |
| /dev/hdc1 | * | 1 | 510 | 4096543+ | 83 | Linux |
| /dev/hdc2 | | 511 | 561 | 409657+ | 82 | Linux swap |