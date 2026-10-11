
## Command free

| Option | Description |
| :--- | :--- |
| used | Used memory (used = total -- free -- buffers - cache) |
| free | Unused memory |
| shared | Memory used by tmpfs (a virtual memory filesystem) |
| buffers | Memory used by kernel buffers |
| cache | Memory used by the page cache |
| buff/cache | Sum of buffers and cache |
| available | An estimation about how much memory is available for new applications. |

Table 3.3: Columns for the command free

Memory in operating systems (not only in Linux) is a complicated topic requiring advanced knowledge about how memory is reserved and shared between different processes. The columns `free` and `available` offer a good overview if the memory in the system is exhausted. The following figure shows the example output for a physical server:

```bash
root@ubuntu:~# free -h
              total        used        free      shared  buff/cache   available
Mem:           31Gi        11Gi       5,8Gi       2,7Gi        13Gi        16Gi
Swap:          31Gi          0B        31Gi
```

Figure 3.14: Output example for the free command with a human-readable format

## Command df

Command `df` (disk free) reports file system disk space usage. This command, without arguments, will show the information for all filesystems and mount points, and indicating an argument will limit the output to that filesystem or mount point. Popular options to filter the result are as follows:

| Option | Option description |
| :--- | :--- |
| -h / --human-readable | Shows information in human readable format instead in kilobytes. |
| -i / --inodes | Shows the number of files in the partition and the available quantity. |
| -l / --local | Excludes remote partitions mounted. |
| -t / --type=TYPE | Filters the list of filesystems to match with the TYPE specified. |
| -T / --print-type | Shows the file system type. |
| -x / --exclude-type=TYPE | Filters the list of filesystems to exclude the TYPE specified. |

Table 3.4: Common options for the command df

The following figure shows the example output showing the human-readable format and the filesystem type information. The following figure is the example output for a Virtual Machine:

```bash
root@ubuntu:~# df -hT
Filesystem            Type   Size  Used Avail Use% Mounted on
tmpfs                 tmpfs  393M  1.2M  392M   1% /run
/dev/mapper/ubuntu--vg-ubuntu--lv
                     ext4     12G  5.0G  5.7G  47% /
tmpfs                 tmpfs  2.0G     0  2.0G   0% /dev/shm
tmpfs                 tmpfs  5.0M     0  5.0M   0% /run/lock
/dev/vda2             ext4   2.0G  126M  1.7G   7% /boot
tmpfs                 tmpfs  393M  4.0K  393M   1% /run/user/1000
```

Figure 3.15: Output example for command df

## Commands lspci, lsusb, and lsblk

These three popular commands are used to display the following information:

- **lspci**: is a utility for displaying information about the PCI buses in the system and devices connected to them. It is possible to obtain more information using the option -v, -vv, or -vvv (more v indicates more verbosity).
- **lsusb**: is a utility for displaying information about USB buses in the system and devices connected to them. This command accepts the option -v to show more advanced information.
- **lsblk**: is a utility to list information about all available or specified block devices, showing partitions for devices, label, and ids for the partitions. It is possible to specify arguments to filter the output to the indicated device (for example, /dev/sda).

## CLI commands to list elements

There are two popular commands to list and find elements such as files, directories, links, or block devices in the system: `ls` and `find`.

### Command ls

The command `ls` lists information about files and directories, listing the current directory if no argument is specified. This command has many options; some of the most useful are described in the following table:

| Option | Option description |
| :--- | :--- |
| -a / --all | Shows hidden files and directories (starting with dot) |
| -c / --color=WHEN | Indicates when colorize the output, can be *always*, *auto* or *never*. |
| -d / --directory | List the directory itself and not the content. |
| -h / --human-readable | Shows the sizes in *human readable* with the more readable unit. |
| -l | Use a long listing format including owner, size and permissions. |
| -r / --reverse | Reverse order while sorting |
| -R / --recursive | List subdirectories recursively. |
| -S | Sort by file size, largest files will be shown first. |
| -t | Sort by time, newest files/directories will be shown first. |
| -1 | List one file per line instead in columns (when option *-l* is not in use) |

Table 3.5: Common options for the command ls

Figure 3.16 shows the command `ls` sorting by size (-S) and in reverse mode (-r), using the long format (-l) and the human-readable (-h).

```bash
root@ubuntu:~/examples# ls -lhSr
total 12K
drwxr-xr-x 2 root root 4.0K Jul  3 20:01 example3
drwxr-xr-x 2 root root 4.0K Jul  3 20:27 example2
drwxr-xr-x 2 root root 4.0K Jul  3 20:00 example1
-rw-r--r-- 1 root root 1.0M Jul  3 20:27 file1M.bin
-rw-r--r-- 1 root root 2.0M Jul  3 20:58 file2M.bin
-rw-r--r-- 1 root root   10M Jul  3 20:29 file10M.bin
```

Figure 3.16: Output example for command ls

### Command find

The command `find` searches for files, directories, or other objects in the system. This command, without options and arguments, will list all the elements recursively under the current directory. It forces to specify first the path and then the expressions to filter. There are multiple options and combinations, and the following table shows some of the most used:

| Option | Option description |
| :--- | :--- |
| -amin n | File was accessed less than, more than or exactly n minutes ago. |
| -atime n | File was last accessed less than, more than or exactly n*24 hours ago. |
| -cmin n | File was changed less than, more than or exactly n minutes ago. |
| -ctime n | File was last changed less than, more than or exactly n*24 hours ago. |
| -mmin n | File was modified less than, more than or exactly n minutes ago. |
| -mtime n | File was last modified less than, more than or exactly n*24 hours ago. |
| -name pattern | Filter the name of the file or directory with the pattern |
| -perm mode | Filter by the permission, useful to find vulnerable files |
| -size n[kMG] | File uses less than, more than or exactly n units. |
| -type c | Filter the type of the file, some of the options are: <br>• b: block special <br>• c: character special <br>• d: directory <br>• f: file <br>• l: link |
| -user username/userid | File is owned by the user or user id specified. |
| -xdev | Don't descend directories on other filesystems. |

Table 3.6: Common options for the command find

The numeric n can be used with +n for greater than n, -n for less than n, and using n only is exactly that value. It is possible to perform different actions with the results using the options -delete, -exec commands as an example or formatting the output with options like -ls or -print0. The following figure shows how to filter files bigger than 1 megabyte:

![](img/863afa537de4eed7deb11978bfbfa90e_98_0.png)

Figure 3.17: Output example for command find

## Explanation of standard streams

In a Linux system, when a command is executed, there are three streams associated: one for the data input, one for the data output, and one for diagnostic or error output. These streams are associated with one name and one integer associated, as shown in the following table:

| Integer | Name | Stream description |
| :--- | :--- | :--- |
| 0 | stdin | Standard input stream, the application receives data using this stream. |
| 1 | stdout | Standard output stream, the data will show the information using it. |
| 2 | stderr | Standard error stream, diagnostic, or errors will show using it. |

Table 3.7: Streams information and integer associated

When a command requires the user to enter data, the application will use the stdin to read what the user will type to introduce the data requested. When the application returns information to the user, it will send it to the standard output (stdout), and if there is any error or diagnostic information to be shown, it will use the standard error (stderr). The following illustration shows the standard streams information:
