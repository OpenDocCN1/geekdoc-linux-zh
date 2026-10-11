/boot:     directory
/bzImage:  x86 boot sector
/cdrom:    directory
/dev:       directory
/etc:       directory
/home:      directory
/lib:       directory
/lost+found: directory
/mnt:       directory
/proc:      directory
/root:      directory
/sbin:      directory
/shlib:     directory
/tmp:       sticky directory
/usr:       directory
/var:       directory
/vmlinuz:   x86 boot sector

Here are some other file types you may find on your system:

/sbin/agetty:   ELF 32-bit LSB executable, Intel 80386, version 1, dynamically linked, stripped
/sbin/explodepkg: Bourne shell script text
/sbin/fsck.ext2: symbolic link to e2fsck
/sbin/initscript.sample: English text
/dev/XOR:       symbolic link to null
/dev/apm_bios:  character special
/dev/aio:       block special
/dev/beep:      character special
/dev/cdrom:     broken symbolic link to cdrom
/dev/gpmdata:   fifo (named pipe)
/dev/hdd12:     block special
/dev/lsdev:     character special
/dev/printer:   socket

# Where Slackware Linux Keeps Files

Just as the rest of UNIX, Slackware Linux keeps its directories and files in a hierarchy. This hierarchy starts with the root directory, / . In the root directory, you have files and subdirectories. The following list shows the directories in the root directory.

```
$ ls -ld /*
drwxr-xr-x    2 root     bin        2048 Aug  6 03:53 /bin
drwxr-xr-x    2 root     root       1024 Aug  6 11:39 /boot
```