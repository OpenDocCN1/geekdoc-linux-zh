# TABLE 14.2

# SWAP MONITORING TOOLS

| Command | Description |
|---|---|
| `/usr/sbin/swap` | The /usr/sbin/swap utility provides a method of adding, deleting, and monitoring the system swap areas used by the memory manager. |
| `/usr/bin/ps` | Use the -a1 options of the /usr/bin/ps command to report the total size of a process currently in virtual memory. The value includes all mapped files and devices, and is reported in pages. These device mappings do not use swap space. |
| `/usr/ucb/ps` | Use this Berkley version of the ps command with the -a1x options to report the total size of a process currently in virtual memory. The value includes all mapped files and devices, and is reported in kilobytes rather than pages. |
| `/usr/bin/vmstat` | Reports virtual memory statistics. |
| `/usr/bin/sar` | System activity reporter. |

The /usr/sbin/swap command has two options that can be used to monitor swap space. The -l option can be used to list swap space. For example:

```
swap -l
```

The system displays the following information listing the details of the systems physical swap space and is described in Table 14.3:

```
swapfile dev swaplo blocks free
/dev/dsk/c0t0d0s3 136,3 16 302384 302384
```

# TABLE 14.3

# OUTPUT FROM THE swap -l COMMAND

| Keyword | Description |
|---|---|
| `<path>` | The pathname for the swap area. In the previous example, the pathname is swapfile. |
| dev | The major/minor device number is in decimal if it is a block special device; zeroes otherwise. |
| swaplo | The swaplo value for the area in 512-byte blocks. swaplo is a kernel parameter that can be modified by the system administrator and represents the offset, in 512-byte blocks, where usable swap space begins. |