
# LAB 58

## Control Mounting and Unmounting of FileSystems: Manual Mounting

**Lab Objective:**

Learn how to manually mount and unmount Linux fileSystems.

**Lab Purpose:**

In this lab, you will learn how to manually mount/unmount fileSystems and how to identify fileSystems via labels and UUID's.

**Lab Tool:**

Ubuntu 18.04 (or another distro of your choice)

**Lab Topology:**

A single Linux machine, or virtual machine

**Lab Walkthrough:**

### Task 1

Open the Terminal and run:

- `lsblk -f`
- `blkid`

These are two commands which can get you information on your block device labels and UUID's. By default your root fileSystem and other fileSystems may not have labels—if they do, `lsblk -f` will print those labels, which can then be passed to `blkid`.

### Task 2

Now run `mount` to identify what fileSystems are currently mounted. If you have an external USB drive, you could insert that, use `lsblk -f` to identify it, and then mount/unmount it with `mount` and `umount`.

### Notes

For information about default fileSystems, see the `/etc/fstab` file and `man fstab`.

# LAB 59

## Control Mounting and Unmounting of Filesystems: Automatic Mounting

**Lab Objective:**

Learn how to automatically mount Linux filesystems.

**Lab Purpose:**

In this lab, you will learn how to automatically mount a filesystem on a Linux system at boot, using the `/etc/fstab` file.

**Lab Tool:**

Ubuntu 18.04 (or another distro of your choice)

**Lab Topology:**

A single Linux machine, or virtual machine

**Lab Walkthrough:**

### Task 1

First, you will need another filesystem to mount. This can be an external disk, or a loopback block device you can create for this purpose (see Lab 56). Identify the label or UUID of this device, then open `/etc/fstab` with your favorite editor. One way to identify the UUID is with `sudo lsblk -f`.

Add a line for this new device. The details will vary based on the device, but here is a template:

```
UUID=01234567-89ab-cdef-0123-456789abcdef  /mnt/mydevice  vfat  defaults  0  2
```

The UUID for my CDROM drive (`sr0`) is listed below:

```
sda
L-sda1  ext4              39584296-303a-4700-a8cd-8386f2f792cb  /
sr0    iso9660  VBox_GAs_5.2.18 2018-08-14-11-58-42-18            /
media/paul/VBox_GAs_5.2.1
```

I then applied the below line to `/etc/fstab`:

```
UUID=2018-08-14-11-58-42-18 /media iso9660 defaults 0 2
```

When in doubt, check the man pages: `man fstab`

Save and close the file, reboot your machine, and check mounted filesystems with `mount`. If you did everything correctly, your device should be mounted!

### Notes

Users with experience in networked filesystems such as NFS may want to read about `autofs`, a tool to automatically mount filesystems as they are needed.

# LAB 60

## Manage File Permissions and Ownership: File Permissions

**Lab Objective:**

Learn how to manipulate permissions and ownership settings of files.

**Lab Purpose:**

In this lab, you will learn to use `chmod`, `chown`, and `chgrp`, as well as `umask`.

**Lab Tool:**

Ubuntu 18.04 (or another distro of your choice)

**Lab Topology:**

A single Linux machine, or virtual machine

**Lab Walkthrough:**

### Task 1

Open the Terminal and run:

```bash
echo "Hello World" > foo
ls -l foo
```

Look at the first field; you should see `rw-r--r--`.

This indicates the user, group, and other permissions. The last nine characters, in groups of three, denote these permissions. In this instance:

- `rw-` indicates read/write (but not execute) permissions for the user who owns the file
- `r--` indicates read-only permissions for the group that owns the file
- `r--` indicates read-only permissions for all non-owners, a.k.a. "world"

The first character indicates the type of file. In this case it is a regular file; directories begin with `d`.

Who are the user and group owners of this file? The third and fourth fields of `ls -l` tell us that. By default, it should be your own user and primary group.

### Task 2

Now run:

- `sudo chown root foo`
- `ls -l foo`
- `cat foo`

You've just changed the user ownership to root, while keeping the group ownership. As the file has group- and world-read permissions, you can still see its contents.

### Task 3

Now run:

- `sudo chmod o-r foo`
- `ls -l foo`
- `cat foo`

That `chmod` command removes read permissions from `foo`. However, as you still have group ownership, you can still see the file's contents.

### Task 4

Now run:

- `sudo chgrp root foo`
- `sudo chmod 600 foo`
- `ls -l foo`
- `cat foo`

This `chmod` command sets the permissions explicitly, to read-write for the owning user only. As that is root, we can no longer read the file.

### Task 5

The default permissions for a newly created file can be adjusted with `umask`. This serves to "mask out," at a bit level, permissions that a new file should not have. Run the following:

- `u=$(umask)`
- `umask 0777`
- `touch bar`
- `ls -l bar`
- `umask $u`

The `bar` file should have no permissions set— you’ve masked them all out with `umask`.

### Task 6

Finally, clean up with `sudo rm foo bar`

### Notes

The first octal bit of `chmod` deals with setuid and setgid (and the sticky bit, on directories). When set, these bits will run an executable file as the user/group owner, rather than the user running the executable. This opens up security risks, particularly when a program is owned by root. For this reason, most systems will ignore the setuid/setgid bits when set on shell scripts.

# LAB 61

## Manage File Permissions and Ownership: Directory Permissions

**Lab Objective:**

Learn how to manipulate permissions and ownership settings of directories.

**Lab Purpose:**

In this lab, you will learn to use `chmod`, `chown`, and `chgrp`, as well as `umask`, and their implications for directories.

**Lab Tool:**

Ubuntu 18.04 (or another distro of your choice)

**Lab Topology:**

A single Linux machine, or virtual machine

**Lab Walkthrough:**

### Task 1

Open the Terminal and run:

```bash
mkdir foo
echo "Hello World" > foo/bar
ls -la foo
```

Look at the first field; you should see `drwxr-xr-x`

This indicates the user, group, and other permissions. The first `d` just indicates a directory. The last nine characters, in groups of three, denote these permissions. In this instance:

- `rwx` indicates read/write/execute permissions for the user who owns the file
- `r-x` indicates read/execute permissions for the group that owns the file
- `r-x` indicates read/execute permissions for all non-owners, a.k.a. “world”

Who are the user and group owners of this file? The third and fourth fields of `ls -la` tell us that. By default, it should be your own user and primary group.

### Task 2

Now run:

- `sudo chown root foo`
- `ls -la foo`
- `cat foo/bar`

You’ve just changed the user ownership to root, while keeping the group ownership. As the directory has group- and world-read permissions, you can still see its contents.

### Task 3

Now run:

- `sudo chmod o-r foo`
- `ls -la foo`
- `cat foo/bar`

That `chmod` command removes read permissions from `foo`. However, as you still have group ownership, you can still see the file’s contents.

### Task 4

Now run:

- `sudo chgrp root foo`
- `sudo chmod 711 foo`
- `ls -ld foo`
- `cat foo/bar`

You’ve now set yourself up with execute-only permissions on the `foo` directory, which is an interesting scenario. You no longer have permissions to view the contents of the directory, nor to add new files to it… but if you already know that a given file exists, your permissions for that file still allow you to act on it. In this example, you can view the contents of `foo/bar`, and even still modify them! This also applies to any subdirectories under `foo`.

### Task 5

Now run:

- `sudo chmod 2777 foo`
- `touch foo/baz`
- `ls -l foo/baz`
