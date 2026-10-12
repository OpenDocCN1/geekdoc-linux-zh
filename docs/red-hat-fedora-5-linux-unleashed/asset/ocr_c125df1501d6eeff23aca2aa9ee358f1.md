# Protect the Contents of User Directories—/home

The most important data on a Linux system resides in user's directories, found under the /home directory. Segregating the system and user data can be helpful in preventing data loss and making the process of backing up easier. For example, having user data reside on a separate file system or mounted from a remote computer on the network might help shield users from data loss in the event of a system hardware failure.

# Use the Contents of the /proc Directory to Interact with the Kernel

The content of the /proc directory is created from memory and only exists while Linux is running. This directory contains special “files” that either extract information from or send information to the kernel. Many Linux utilities extract information from dynamically created directories and files under this directory, also known as a virtual file system. For example, the free command obtains its information from a file named meminfo:

```
$ free
```text
        total         used       free     shared      buffers     cached
Mem:      255040      250752       4288          0         1716       90964
-/+ buffers/cache:    158072       96968
Swap:       524280        760      523520
```
```

This information constantly changes as the system is used. You can get the same information by using the cat command to see the contents of the meminfo file:

```
$ cat /proc/meminfo
```text
MemTotal:     255040 kB
MemFree:       4412 kB
Buffers:       2164 kB
Cached:        90580 kB
SwapCached:     0 kB
Active:        208884 kB
Inactive:       8976 kB
HighTotal:      0 kB
HighFree:       0 kB
LowTotal:     255040 kB
LowFree:        4412 kB
SwapTotal:    524280 kB
SwapFree:     523520 kB
Dirty:          40 kB
Writeback:      0 kB
Mapped:        201520 kB
Slab:          24772 kB
CommitLimit:   651800 kB
Committed_AS:  341544 kB
PageTables:    2880 kB
VmallocTotal:  770040 kB
VmallocUsed:   3432 kB
```
```