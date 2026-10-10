environment, making for lots of individual commands you have to know. Fortunately, a common frontend program can determine the filesystem on the storage device and use the appropriate filesystem recovery command based on the filesystem being recovered.

The fsk command is used to check and repair most Linux filesystem types, including ones discussed earlier in this chapter. The format of the command is

```
fsck options filesystem
```

You can list multiple filesystem entries on the command line to check. Filesystems are referenced using several methods, such as the device name or its mount point in the virtual directory. However, the device must be unmounted before you use fsk on it.

> **Tip**
> Although you can use the fsck command on journaling filesystems, it is arguable as to whether filesystems that employ COW need it. In fact, the ZFS filesystem does not even have an interface to the fsck utility. The fsck.xfs and fsck.btrfs commands are nothing but stubs, and they do nothing. For COW filesystems, check the man pages for their individual filesystem repair tool(s), if you need advanced repair options.

The fsck command uses the /etc/fstab file to automatically determine the filesystem on a storage device that’s normally mounted on the system. If the storage device isn’t normally mounted (e.g., if you just created a filesystem on a new storage device), you need to use the -t command-line option to specify the filesystem type. Table 8.5 lists the other commonly used command-line options available.

# TABLE 8.5 The fsck Commonly Used Command-Line Options

| Option | Description |
| :----- | :------------------------------------- |
| -a | Automatically repairs the filesystem if errors are detected |
| -A | Checks all the filesystems listed in the /etc/fstab file |
| -N | Doesn’t run the check; only displays what checks would be performed |
| -r | Prompts to fix if errors found |
| -R | Skips the root filesystem if using the -A option |
| -t | Specifies the filesystem type to check |
| -V | Produces verbose output during the checks |
| -y | Automatically repairs the filesystem if errors are detected |


You may notice that some of the command-line options are redundant. That’s part of the problem with trying to implement a common frontend for multiple commands. Some of the individual filesystem repair commands have additional options that can be used.