common front-end program can determine the filesystem on the storage device and use the appropriate filesystem recovery command based on the filesystem being recovered.
The `fsck` command is used to check and repair most Linux filesystem types, including ones discussed earlier in this chapter. The format of the command is

```
fsck options filesystem
```

You can list multiple `filesystem` entries on the command line to check. Filesystems are referenced using several methods, such as the device name or its mount point in the virtual directory. However, the device must be unmounted before you use `fsck` on it.

![](bbox=[0.11, 0.36, 0.89, 0.62])

The `fsck` command uses the `/etc/fstab` file to automatically determine the filesystem on a storage device that's normally mounted on the system. If the storage device isn't normally mounted (e.g., if you just created a filesystem on a new storage device), you need to use the -t command-line option to specify the filesystem type. <span style='color:blue;font-weight:bold'>Table 8-5</span> lists the other commonly used command-line options available.

# <span style='color:blue'>TABLE 8-5</span> <span style='font-weight:bold'>The `fsck` Commonly Used Command-Line Options</span>

| Option | Description |
| ------ | ----------- |
| -a | Automatically repairs the filesystem if errors are detected. |
| -A | Checks all the filesystems listed in the /etc/fstab file. |