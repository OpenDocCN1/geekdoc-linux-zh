```
```text
fcsk -A
```
```

This command checks and repairs all file systems specified in the `/etc/fstab` file. It's often used during the system boot process.

# ### 5. Check a Specific File System Type:

```
```text
fcsk.ext4 /dev/sda1
```
```

In this example, `fcsk.ext4` is used specifically for the ext4 file system. Different file systems may have their own `fcsk` variants.

# ### 6. Force File System Check Even if Clean:

```
```text
fcsk -f /dev/sda1
```
```

The `-f` option forces a file system check even if it appears clean. This can be useful for ensuring a thorough examination.

# ### 7. Check and Repair Root File System: