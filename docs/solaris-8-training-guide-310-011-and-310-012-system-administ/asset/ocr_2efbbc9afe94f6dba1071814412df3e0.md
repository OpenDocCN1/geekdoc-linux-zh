# TABLE 7.8

# Volume Manager Directories and Links

| Link | Description |
|---|---|
| /vol/dev/diskette0 | The directory providing block device access for the medium in floppy drive 0 |
| /vol/dev/rdiskette0 | The directory providing character device access for the medium in floppy drive 0 |
| /vol/dev/aliases/floppy0 | The symbolic link to the character device for the medium in floppy drive 0 |
| /dev/rdiskette | The directory providing character device access for the medium in the primary floppy drive, usually drive 0 |
| /vol/dev/aliases/cdrom0 | The directory providing character device access for the medium in the primary CD-ROM drive |
| /vol/dev/dsk/ | The directory providing access to the CD-ROM buffered, or block, device |
| /vol/dev/rdsk/ | The directory providing access to the CD-ROM character, or raw, device |
| /cdrom/cdrom0 | The symbolic link to the buffered device for the medium in CD-ROM drive 0 |
| /floppy/floppy0 | The symbolic link to the buffered device for the medium in floppy drive 0 |

The vold daemon automatically mounts CD-ROM and file systems when removable media containing recognizable file systems are inserted into the devices. When a CD is inserted, vold automatically mounts the CD-ROM file system into the /vol/dev directories just described. With a floppy disk, however, the floppy's file system is not automatically mounted until you issue the volcheck command. The volcheck command instructs vold to look at each device and determine if new media has been inserted into the drive. On floppy disks, don't have vold continually poll the disk drive like it does on a CD because of the hardware limitation in floppy drives. Continuously polling of a floppy disk for media causes a mechanical action in the floppy disk drive and causes the drive to wear out prematurely.

The vold daemon is the workhorse behind Volume Manager. It is automatically started by the /etc/init.d/volmgt script. vold reads the /etc/vold.conf configuration file at startup. The vold.conf file contains the Volume Manager configuration information that vold uses.