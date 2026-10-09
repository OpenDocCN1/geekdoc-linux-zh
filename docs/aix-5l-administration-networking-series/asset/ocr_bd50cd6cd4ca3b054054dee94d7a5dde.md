# Block Size

Block size is an important consideration and will affect the total media capacity and the time required to read or write data on the device. Larger block sizes reduce the number of interrecord gaps and make better use of the tape. The block size should also reflect the physical block size written by the device. For example, an 8 mm tape drive writes 1024 bytes per block diagonally across the width of the tape. If the block size defined to AIX for the device is fixed at 512 byte blocks, then the device will write out 512 bytes of data and pad the remaining 512 bytes in the physical 1024-byte block. This effectively reduces the media capacity by half, and restores will take twice as long. When variable-length blocks are defined in AIX for the example 8 mm device, block sizes larger than 1024 will fill each physical block on the tape. If the block size used by the application is not a multiple of 1024, then the last physical block written will be padded.

Block size is application dependent. Selecting the wrong block size can inhibit the ability to read backup media and cause portability problems. IBM’s **mkssysb** script changes the block size to 512 bytes for the first three images (boot, bosinst, and to c) of a bootable system backup tape and then restores the previous block size before backing up the rootvg volume group to the fourth image. The **savevg** command is a symbolic link to the **mkssysb** script that will not change the tape device block size or create the boot, bosinst, and toc images when backing up non-rootvg volume groups.  
You can change the default block size defined to AIX for a tape device using the **chdev** command or through SMIT, as shown in the following listing. Remember that this does not alter the physical block size used by the device!

```
```text
# chdev -l rmt0 -a "block_size=0"                 Variable block size
# chdev -l rmt0 -a "block_size=512"              Fixed 512-byte block size
# chdev -l rmt0 -a "block_size=1024"             Fixed 1024-byte block size
```
```

Or you can use the SMIT FastPath **smit chtgtpe**.

```
```text
# dd if=/dev/rmt0.1 ibs=64k obs=512 | restore -xvb
# dd if=/dev/rmt0.1 ibs=64k obs=5120 | tar -xvBf-
# dd if=/dev/rmt0.1 ibs=64k obs=5120 | cpio -iVB
```
```

If portability is an issue, you will want to define a default block size of 0, which indicates a variable block size. Byte ordering and ASCII/EBCDIC conversion can be handled by the **conv** option to the **dd** command.

```
```text
# dd if=/dev/rmt0 conv=swab                      Swap byte pairs
# dd if=/dev/rmt0 conv=ascii                    Convert EBCDIC to ASCII
# dd if=/dev/rmt0 ibs=512 obs=1024 conv=sync    Pad blocks
```
```

Table 10-1 provides a few hints when using **tar** to move data from an RS/6000 or pSeries machine to one of the listed vendor types.