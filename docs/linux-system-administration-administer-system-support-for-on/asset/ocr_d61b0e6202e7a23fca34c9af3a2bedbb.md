+   3. Stick in the disk.

+   4. Mount the directory.

I have one floppy drive, so I can show you the steps I go through to mount it on a Linux system. First, to look at what's already mounted, use the mount command.

```
# mount
/dev/hda1 on / type ext2 (rw)
/dev/hda2 on /home type ext2 (rw)
/dev/hda3 on /opt type ext2 (rw)
none on /proc type proc (rw)
```

Look - no floppy drive mounted (you can't see /dev/fd0 on the list of drives). If I'm mounting the drive for the first time, I would have to create a directory to serve as a mount point for the floppy drive (say, one creatively called /floppy). You can call your drive whatever you want - /dosa (since the drive is recognized as msdos file format), /fred, /mom - and our practical example looks like this:

```
# mkdir /floppy
```

When you've created the directory, mount the drive:

```
# mount /dev/fd0 /floppy/
```

If it mounts properly, you won't see any error messages and you'll return to the prompt. If you want to double-check to see whether your drive mounted properly, type the mount command again. The result would resemble the following snippet:

```
# mount
/dev/hda1 on / type ext2 (rw)
/dev/hda2 on /home type ext2 (rw)
/dev/hda3 on /opt type ext2 (rw)
none on /proc type proc (rw)
/dev/fd0 on /floppy type msdos (rw)
```

The drive is mounted; if you do an ls on the /dev/fd0 next, here's what you get:

```
# ls /dev/fd0
/dev/fd0
```

Not much. What you need to do is an ls on the mount point - in this case, /floppy, as follows: