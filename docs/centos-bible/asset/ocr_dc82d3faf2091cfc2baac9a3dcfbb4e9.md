The `growisofs` command is also nice for backups because it has simple options for doing multisession DVDs. For example, if you want to back up your /home/timothy directory today, then back up your /var/www directory later, you start the first backup as follows:

```
```
$ growisofs -Z /dev/cdrom -R -J /home/timothy
```
```

The `-Z` indicates that this is an initial session being written to the CD or DVD. The device of the CD/DVD drive is `/dev/cdrom`. The `-R` and `-J` options allow longer Linux filenames on ISO9660 images (so the disk can be read by other operating systems; you still retain Linux extensions). The last option (in this case, /home/timothy) is whatever directories or files you want to copy to DVD.

When you are ready to write more to the CD or DVD, use the `-M` option instead, to indicate that you are adding on to an existing CD or DVD. Here is an example:

```
```
$ growisofs -M /dev/cdrom -R -J /var/www
```
```

Here, the `-M` indicates to add a new session to the existing session on the CD or DVD. The content of the /var/www directory (and its subdirectories) is written to the media. You can mount the media between sessions. Just be sure to unmount it before you try to write to it again (using the `umount` command).

# # Backing Up to a Hard Drive

As noted in the simple backup procedure in the beginning of this chapter, removable media such as tapes, DVDs, and CDs are not the only choice for backing up your data. You may find it useful to install a second hard drive in your system and use that drive for backups. This has several advantages over other backup media:

+   * Data can be backed up quickly and throughout the day; thus, backed-up data will be more current in the event of a crash.
+   * There's no medium to load. Data can be located and recovered more quickly.
+   * You can configure the second disk to be a virtual clone of the first one. If the first disk crashes, you can simply boot off the second disk rather than installing new hardware. With disk mirroring software, this process can even be automated. The downside to this approach is that a mirrored drive that is online all the time is more prone to error than would be the case when copying files to removable media, and then removing the media to a safe location.
+   * With new, cost-effective removable hard drives (including those connected via USB and FireWire), you have the convenience of removable media with what was once usually thought of as non-removable media.