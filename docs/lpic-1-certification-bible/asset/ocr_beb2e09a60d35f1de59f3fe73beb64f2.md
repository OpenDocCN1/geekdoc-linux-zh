# **Table 6-8**

**Options Used with dd**

| Option | Use |
| :--- | :--- |
| `if=FILE` | Specifies the location of a source to use instead of standard input. This is the input file. |
| `of=FILE` | Specifies the location of the destination to use instead of standard output. This is the output file. |
| `ibs=BYTES` | Specifies the number of *BYTES* read at a time. |
| `obs=BYTES` | Specifies the number of *BYTES* written at a time. |
| `bs=BYTES` | Specifies the number of *BYTES* to read and write at a time. |
| `cbs=BYTES` | Specifies the number of *BYTES* to convert at a time. |
| `skip=BLOCKS` | Specifies the *BLOCKS* to skip in the input file before copying. |
| `seek=BLOCKS` | Specifies the *BLOCKS* to skip in the output file before writing. |
| `count=BLOCKS` | Specifies the *BLOCKS* of the input file to copy instead of copying the entire file. |

The `dd` command can be used for a variety of special tasks. For example, suppose the system you currently use is running both Windows NT and Windows 98. The first partition contains Windows 98 system files and is formatted with FAT. The second partition contains Windows NT system files and is formatted with NTFS. A third partition, formatted as FAT, contains data that is shared between the two operating systems. This drive also contains 3GB of space that you wish to use for Linux. Because this computer is used by your young children, you prefer to use the NT boot loader that they are familiar with using. This can be done by installing the Linux boot sector along with LILO to a location that doesn't overwrite the master boot record; in this case you install the Linux boot partition to `/dev/hda5`. While in Linux, mount the Windows 98 system partition so that you can write to it. Then run the following command:

```
# /bin/dd if=/dev/hda5 bs=512 count=1 of=/mnt/win_c/bootsek.lin
```

This will create a file named `bootsek.lin` on the Windows 98 system partition. The file will be written as one block with a size of 512 bytes. You will then need to boot to either NT or Windows 98 and edit the `boot.ini` file to include the following line:

```
c:\bootsek.lin="Linux"
```

This will add a line to the NT boot loader for Linux. When this line is selected during boot, the system will then boot to the LILO boot loader. Any time the `lilo` command is run on the Linux system the `bootsek.lin` file will need to be rewritten.