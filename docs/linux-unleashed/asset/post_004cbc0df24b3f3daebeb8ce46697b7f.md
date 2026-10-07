
# Map Installer Configuration File Options

Configuration options for the map installer can be stored in the file /etc/lilo/config. The file consists of sets of parameter-value pairs, although some options do not need a value. Whitespace can be used between parameters, the equal sign, and the value. Comments can be included by starting the line with a pound sign. A newline character terminates the comment.

As a rule, variable names are not case sensitive, whereas values usually are. It is good practice, though, to keep all entries lowercase (as is UNIX convention).

The options shown in Table 4.3 can be put into the map installer configuration file /etc/lilo/config.

**TABLE 4.3. MAP INSTALLATION OPTIONS.**

| Option | Meaning |
| :----- | :------ |
| i sector | Installs the kernel as the new boot sector. Can be read from the install configuration variable. |
| I name | Displays the path of the name kernel image file. If no matching name is found, an error is generated. The option “v” can be added after the name to verify the existence of the image file. This option uses the `BOOT_IMAGE` environment variable. |
| l | Generates linear sector addresses instead of the default `sector/head/cylinder` addresses. Can also be specified with the configuration variable `linear`. |
| m file | Uses `file` as the location of the map file. If no filename is given, `/etc/lilo/map` is used. |
| P fix | Allows LILO to adjust sector/head/cylinder addresses using the table file. Also specified with the `fix table` configuration variable. |
| P ignore | Overrides correction of sector/head/cylinder addresses. Also specified with the `ignore table` configuration variable. |
| q | Displays the currently mapped files. |
| r dir | Performs a `chroot` command on `dir` before continuing. This is necessary if the root file system is mounted in a different location from the map installer command. Because the current directory is changed with this command, use absolute pathnames for all files. |
| R words | Stores words in the map file for use by the boot loader. The words are parameters used by the boot process as part of the default command line. The first word must be the name of the boot image. |
| s file | Copies the original boot sector to `file` instead of `/etc/lilo/boot.hex_num`. |
| S file | Same as `s` but overwrites the old file if it exists. |
| t | Performs a test by executing the entire installation process except writing the map file and boot sector. Ideally used with the `v` option to verify accurate behavior of the map installer. |
| u dev | Restores the backup copy of the boot sector for `dev`. If no device is specified, the default value is used or, failing a valid value, the current root device. The backup copy is checked for a time stamp before the write is completed. |
| U dev | Same as `u` except no check for the time stamp. |
| v level | Uses the verbose output level specified to display messages. |
| V | Displays the version number of the map installer, then exits. |
| alias=name | Allows an image to be called by the string name as well as its normal filename. |
| append=string | Appends string to the command line passed to the kernel. Mostly used to pass boot parameters about hardware devices that are not automatically detected by the kernel. |
| backup=file | Copies the original boot sector to file instead of /etc/lilo/boot.hex_num. Can also be a device (like /dev/null). |
| boot=dev | Specifies the device that contains the boot sector. If no name is specified, the currently mounted root partition is used. |
| compact | Merges read requests for adjacent sectors into a single read request, reducing the load time and file size. This is commonly used with floppy disks. |
| delay=secs | Gives the delay in tenths of a second to wait before booting the image. If no delay is given, boot is immediate. |
| disktab=file | Gives the name of the disk parameter table. If no filename is given, /etc/lilo/disktab is used. |
| fix-table | Lets LILO adjust sector/head/cylinder addresses. Usually used with operating systems that may change these addresses. LILO will readjust incorrect entries if fix-table is specified. |
| force-backup=file | Similar to backup, but overwrites any existing file. If force-backup is used in the configuration options, any backup option is ignored. |
| install=sector | Installs the image in the specified boot sector. If no value is given, /etc/lilo/boot.b is used. |
| label=name | Renames an image to the alternate string name. |
| linear | Generates linear sectors instead of sector/head/cylinder addresses. Linear addresses are independent of disk geometry and are translated in real time. Linear boot disks may not be portable. |
| literal=string | Similar to the append variable but removes any other options, using only those specified in string. |
| map=file | File is the map file location. If no value is given, /etc/lilo/map is used. |
| message=file | Uses the file contents as a message displayed before the boot: prompt. The message cannot be larger than 64Kb. If the message is changed or moved, the map file must be rebuilt. |
| optional | Makes an image optional. If the image’s file can’t be located, it is not booted. This is useful for testing new kernels. |
| password=password | Sets a password for all images. If the option that is restricted exists, a password is required only to boot the image the configuration file refers to. |
| prompt | Forces the boot: prompt without checking for any keypresses. Usually combined with timeout to force unattended reboots. |
| ramdisk=size | Sets the optional RAM disk to size. Setting equal to zero suppresses the RAM disk. |
| read-only | Mounts the root file system as read-only. |
| read-write | Mounts the root file system as read-write. |
| restricted | Relaxes password protection. |
| root=dev | Specifies the device to be mounted as the root file system. If the value current is used, the root device is the device on which the root file system is currently mounted (unless changed with the -r command-line option). |
| serial=params | Sets a serial line for control, initializing the line and accepting input from it (as well as the console). The format of the parameters is port, baud_rate, parity, bits. When serial is set, the delay value is set to 20 automatically, unless overridden. |
| timeout=secs | Sets the number of tenths of seconds to wait for keyboard input before loading the image. Also used to specify password input timeouts. Default value is infinite. |
| verbose=level | Displays progress messages. The higher the level, the more messages. If the -v command line option is also included, the higher level is used. |
| vga=mode | Sets the VGA text mode for use during booting. Valid values are normal (80x25 text mode); extended or ext (80x50 text mode); ask (prompt for the mode during boot); and any valid text mode value. To obtain a list of available modes, boot with the parameter vga=ask and press Enter when asked for a value. Case is not important in the values of the vga option. |

If any parameter is not specified either on the command line or in the configuration file, default values are used. Some values are also maintained within the kernel image (such as ramdisk, root, and vga).

# Boot Images

LILO can boot a kernel image from several locations, such as a regular file on the root file system or any other mounted file system, from a block device such as a floppy disk, or from the boot sector of another partition or disk. The type of boot is dictated by entries in a configuration file.

Boot image configuration files can have several variables defined, all of which have been mentioned previously. Valid configuration file variables are alias, label, optional, password, ramdisk, read-only, read-write, restricted, root, and vga.

To boot a kernel image from a file, all that is necessary in the configuration file is the name of the image. For example, the following line boots the image called linux_main:

```
image=/linux_main
```

To boot an image from another device, the sectors that must be read on that device have to be specified. There are several methods of providing the sector information. The starting sector must be provided, but you can then either specify a number of sectors to be read (start+length) or the end sector number (start-finish). If only one number is provided (the start sector), only that sector is read.

For example, the contents of this configuration file boot the kernel from the floppy disk, starting at sector 1 and reading the next 512 sectors:

```
image=/dev/fd0
range=1+512
```

More than one configuration can be specified for an image because LILO stores values in an image descriptor file and not in the image itself. For example, a configuration file can contain the following entries:
