# Duration

This task should take about half an hour to complete. A single run of `fsck` can take anywhere from a few seconds to many minutes (perhaps even over an hour), depending on the size of the filesystem, the speed of the disk, the number of files stored on the filesystem, and so on.

# Setup

You should have access to the disk you prepared in Tasks 5.2 and 5.3 or to some other convenient partition that's not required for system operation. (If necessary, you can create a filesystem on a floppy disk and use it to complete this task.) You must have superuser access to check a filesystem, so log in and acquire **root** privileges.

# Caveats

The usual caveats concerning **root** access apply to this task. Beyond these cautions, checking a filesystem is theoretically safe, even if you accidentally enter the wrong partition device code. Checking a filesystem that's currently mounted, though, is not safe; changes made by the filesystem check code can cause the kernel to become confused and result in additional corruption. Fortunately, `fsck` checks to see if you're calling it on a mounted filesystem and warns you about this. Be sure to read all the messages displayed by `fsck` as it operates. If you see a warning you don't understand or that causes you concern, tell the software to stop and research that message before proceeding.

# Procedure

To perform a disk check, you use the filesystem check (`fsck`) program. Ordinarily, its use is fairly straightforward. On occasion, though, you might want to use additional tools to give your filesystem a tune-up.

# Basic Disk Checking

To check the integrity of a filesystem and automatically repair any damage, you can pass the device filename to `fsck`. If necessary, unmount the filesystem first:

```
```bash
# umount /dev/sda1
# fsck /dev/sda1
```
```

> As noted earlier, you should be sure the filesystem is unmounted before using `fsck`. Failure to unmount the filesystem can, paradoxically, cause filesystem damage.

The `fsck` program, like `mkfs`, is actually a front end to other programs, named `fsck.<span>f</span>ilesystem`, where `<span>f</span>ilesystem` is the filesystem name. Some filesystem utility packages provide additional links to their filesystem check programs, such as `e2fsck` for ext2 and