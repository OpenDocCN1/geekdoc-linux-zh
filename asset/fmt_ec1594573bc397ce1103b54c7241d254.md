
## LAB 55

### Basic File Editing: `vi` Modes

**Lab Objective:**

Learn how to use modes within the `vi` editor.

**Lab Purpose:**

In this lab, you will learn about one of the classic (but often opaque to new users) Linux text editors, `vi`.

**Lab Tool:**

Ubuntu 18.04 (or another distro of your choice)

**Lab Topology:**

A single Linux machine, or virtual machine

### Lab Walkthrough:

#### Task 1

Open the Terminal and run `vi Tab55.txt`. Now, explore the modes of `vi`:

- Type `i` to enter insertion mode, and enter a few lines of text. Type `ESC` to leave this mode.
- Navigate to the middle of a line and type `a` to enter insertion mode one character after the cursor's position. Enter more text or hit `ESC` to exit the mode.
- Navigate to the middle of a line and type `I` to insert text at the beginning of this line. Hit `ESC` to exit insertion mode.
- Type `A` to add text at the end of the current line. Again, hit `ESC` to exit.
- Navigate to a line and type `o` to add a line of text below it. Hit `ESC` to exit insertion mode.
- Type `O` to add a line of text above the line where your cursor is. Again, hit `ESC` to exit.
- Use `y` to copy ("yank") text; for example, `y$` to yank from the cursor to the end of a line, or `yy` to yank the whole line. Then, press `p` to paste.
- Use `d` to delete text; for example, `d$` to delete from the cursor to the end of a line, or `dd` to delete the whole line. Type `x` a few times to delete a few characters under the cursor.
- Finally, use `:q!` to quit, or if you’ve written something useful, `:w!` to save it. You may also use `:wq`, `:x`, or `ZZ` to save and quit.

**Notes:**

Hopefully, you can see that there is symmetry among `vi` commands—`a`/`A`, `o`/`O`, `y`/`yy` and `d`/`dd`, etc. Now that you’re a `vi` pro, install and try its improved version, `vim`!

## LAB 56

### Create Partitions and Filesystems

**Lab Objective:**

Learn how to configure disk partitions and filesystems.

**Lab Purpose:**

In this lab, you will learn about partitioning disks using tools such as `parted`, and creating filesystems with tools such as `mkfs`.

Note: `fdisk` was covered extensively in Lab 32, and so will not be covered here. It is recommended to do Lab 32 to learn more about `fdisk`.

**Lab Tool:**

Ubuntu 18.04 (or another distro of your choice)

**Lab Topology:**

A single Linux machine, or virtual machine

### Lab Walkthrough:

#### Task 1

The first step is to create a dummy block device to be used in the rest of the lab, so you don't erase any of your machine's actual data. Open a terminal and run:

```bash
dd if=/dev/zero of=block.img bs=100M count=10
```

This file is only 1GB in size. It doesn't need to be large, but if you have more space you can make it larger for more flexibility. Now run:

- `sudo losetup -fP block.img`
- `losetup -a | grep block.img | cut -d: -f1`

This should print a device name such as `/dev/loop0`. This is the loopback block device, and is what should be substituted everywhere you see `[dev]` for the rest of this lab.

#### Task 2

Now you will partition this new block device. `gdisk` is a useful tool for creating GPT partition tables. It is based on `fdisk` and the syntax is nearly identical, so please reference Lab 32 to learn about `gdisk`. For now, use `parted` instead:

```bash
sudo parted [dev]
```

You can use `parted` non-interactively, but here, run the following commands in interactive mode:

- `mklabel gpt`
- `mkpart primary ext4 0 50%`
- `mkpart primary linux-swap 50% -1s`
- `quit`

These changes may prompt some warnings; they are not important for this case and you should respond in the affirmative.

It is worth noting that, unlike `fdisk` and `gdisk`, `parted` does not store all changes in memory and write them at the end, but writes every change made as you make it. Thus, it might be considered less safe than the previous two.

#### Task 3

Now create an ext4 filesystem on the first partition of your block device. The name should end in “p1”—for example, if your block device is `/dev/loop0`, the first partition should be `/dev/loop0p1`:

```bash
sudo mkfs.ext4 [dev]p1
```

Finally, create a swap partition as well: `sudo mkswap [dev]p2`

If you were actually setting up a new system, you would then activate the swap partition with `swapon`, but in this case you should not do that. You could also mount the `[dev]p1` partition, and start using it as a normal ext4 filesystem if you wanted to.

#### Task 4

Clean up:

- `sudo losetup -d [dev]`
- `rm block.img`

### Notes

In this lab you only created an ext4 filesystem—ext4 is one of the most common filesystems used on Linux today, but it is far from the only option. Under what circumstances might you choose XFS, VFAT, exFAT, or Btrfs, instead?

## LAB 57

### Maintain the Integrity of Filesystems

**Lab Objective:**

Learn how to verify filesystem integrity and repair basic problems.

**Lab Purpose:**

In this lab, you will use tools such as `fsck` and `xfs_repair` to search for filesystem problems, as well as learn how to monitor free space and inodes.

**Lab Tool:**

Ubuntu 18.04 (or another distro of your choice)

**Lab Topology:**

A single Linux machine, or virtual machine

### Lab Walkthrough:

#### Task 1

First, set up a dummy block device for use in the rest of this lab:

- `dd if=/dev/zero of=block.img bs=100M count=10`
- `sudo losetup -fP block.img`
- `losetup -a | grep block.img | cut -d: -f1`

This should print a device name such as `/dev/loop0`. This is the loopback block device, and is what should be substituted everywhere you see `[dev]` for the rest of this lab (ignore all warnings you may see for `parted`).

Continue with:

- `sudo parted [dev] mklabel gpt`
- `sudo parted [dev] mkpart primary ext4 0 50%`
- `sudo parted [dev] "mkpart primary xfs 50% -1s"`
- `sudo mkfs.ext4 [dev]p1`
- `sudo apt -y install xfsprogs`
- `sudo mkfs.xfs [dev]p2`
- `mkdir lab57-ext4 lab57-xfs`
- `sudo mount [dev]p1 lab57-ext4`
- `sudo mount [dev]p2 lab57-xfs`
- `sudo dd if=/dev/urandom of=lab57-ext4/random bs=1M count=500`
- `sudo dd if=/dev/urandom of=lab57-xfs/random bs=1M count=500`
- `md5sum lab57-{ext4,xfs}/random`

What you've just done is created two filesystems on your block device and filled them up with a file containing random data. Then you obtained the md5 hash of each file, which you should save for later.

#### Task 2

Now, you get to do something you would never do on a live system... cause damage, intentionally!

- `sudo umount [dev]p1 [dev]p2`
- `sudo dd if=/dev/urandom bs=1 count=10M of=[dev]p1 seek=1M`
- `sudo dd if=/dev/urandom bs=1 count=10M of=[dev]p2 seek=1M`

You've just caused some significant corruption to both filesystems, though unfortunately because of the nature of such corruption, the results can't be predicted. What you should do is attempt to remount both filesystems and get the MD5 sums again:

- `sudo mount [dev]p1 lab57-ext4`
- `sudo mount [dev]p2 lab57-xfs`
- `md5sum lab57-{ext4,xfs}/random`

However, it's possible that `md5sum` or even `mount` will fail for one or both filesystems. Make sure the filesystems are unmounted again, then run:

- `sudo fsck [dev]p1`
- `sudo xfs_repair [dev]p2`

You should then be able to mount the filesystems again. However, you may notice that the MD5 sums of your "important" data have been permanently altered. This is the unfortunate fact of filesystem corruption--not everything can always be saved.

#### Task 3

Check disk space on both filesystems with:

- `du -hs lab57*`
- `df -h [dev]*`

Are they still full, or were one or both of your files actually deleted because of the corruption?

#### Task 4

Finally, clean up:

- `sudo umount lab57*`
- `sudo losetup -d [dev]`
- `rm block.img`
- `rmdir lab57*`

### Notes

Both ext4 and XFS have advanced tuning parameters for a variety of needs. See the man pages for `tune2fs`, `xfs_fsr`, and `xfs_db`.
