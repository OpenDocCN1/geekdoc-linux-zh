| Block size: | 4096 |
| Fragment size: | 4096 |
| Group descriptor size: | 64 |
| Reserved GDT blocks: | 1024 |
| Blocks per group: | 32768 |
| Fragments per group: | 32768 |
| Inodes per group: | 8192 |
| Node blocks per group: | 512 |
| Flex block group size: | 16 |
| Filesystem created: | Mon Jun 17 13:49:59 2019 |
| Last mount time: | Fri Jun 28 21:14:38 2019 |
| Last write time: | Mon Jun 17 13:53:39 2019 |
| Mount count: | 8 |
| Maximum mount count: | -1 |
| Last checked: | Mon Jun 17 13:49:59 2019 |
| Check interval: | 0 (<none>) |
| Lifetime writes: | 20 GB |
| Reserved blocks uid: | 0 (user root) |
| Reserved blocks gid: | 0 (group root) |
| First inode: | 11 |
| Inode size: | 256 |
| Required extra isize: | 32 |
| Desired extra isize: | 32 |
| Journal inode: | 8 |
| First orphan inode: | 5117383 |
| Default directory hash: | half_md4 |
| Directory Hash Seed: | fa95a22a-ai19-4667-a73e-78f77af6172f |
| Journal backup: | inode blocks |
| Checksum type: | crc32c |
| Checksum: | 0xe084fe23 |

ext filesystems have mount counts. The count is increased by 1 each time the filesystem is mounted, and when a threshold value (the maximum mount count) is reached the system will be automatically checked with e2fsck on the next boot.

The maximum mount count can be set with the -c N parameter, where N is the number of times the filesystem can be mounted without being checked. The -C N parameter sets the number of times the system has been mounted to the value of N. Note that command line parameters are case-sensitive, so -c is different from -C.

It is also possible to define a time interval between checks, with the -i parameter, followed by a number and the letters d for days, m for months and y for years. For example, -i 10d would check the filesystem at the next reboot every 10 days. Use zero as the value to disable this feature.