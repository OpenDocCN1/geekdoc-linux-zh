would result from a `dir C:` command under DOS. You can use `cd` to see other directories under `/dos` and use any Linux command to slice and dice your DOS files.

It’s great to have the ability to copy files back and forth between Linux and DOS, but you can also do some clever things if you think creatively. I find it particularly helpful to use the `ln` (link) command to share my Netscape bookmarks file between Linux and DOS, like this:

```
`ln -s /dos/netscape/bookmark.htm $HOME/.netscape/bookmarks`
```

By linking these files together, I need to manage just one bookmark file. Of course, this trick works only if both the DOS and Linux versions of a product use the same format for the files being shared.

If you want your DOS partition to mount each time you boot Linux, add the line shown here to the `/etc/fstab` file:

```
`/dev/hda1  /dos  msdos  umask=022`
```

When Linux boots up, it looks in the `/etc/fstab` file and mounts all the file systems specified there, so you won’t have to issue the mount command manually to access your DOS partition. The line you just added to `/etc/fstab` has the same effect as the mount command shown earlier. The same caveat about FAT32 file systems applies here, so you may need to replace `msdos` with `vfat` in the previous example.

# RUNNING DOS PROGRAMS WITH DOSEMU

DOSemu (DOS Emulator) is a program that lets you run many of your favorite DOS applications under Linux. The name is a little bit misleading—it doesn’t actually emulate DOS; it boots DOS to a virtual machine using the special hardware features in Intel 80386 and higher CPUs.

A DOSemu session looks and acts like a real DOS session, with a few limitations on what can be done. Not all video and sound cards are supported under DOSemu, and some programs that require DPMI (DOS Protected-Mode Interface) will not run. The most notable example of this is Windows 3.1, although some people do report being able to run it under DOSemu.