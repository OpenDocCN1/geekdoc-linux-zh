
### OPTIONS

- **-T**, **--print-type**: Print a type string for each filesystem. Any such printed filesystem type name may be used as an argument to either of the **--type=** or **--exclude-type=** options.
- **-t**, **--type=fstype**: Limit the listing to filesystems of type fstype. Multiple filesystem types can be shown by giving multiple -t options. By default, all filesystem types are listed.
- **-x**, **--exclude-type=fstype**: Limit the listing to filesystems not of type fstype. Multiple filesystem types can be eliminated by giving multiple -x options. By default, all filesystem types are listed.
- **-v**: Ignored; for compatibility with System V versions of df.
- **--help**: Print usage message on standard output and exit successfully.
- **--version**: Print version information on standard output then exit successfully.

## DU(1)

### NAME

**du**: Summarize disk usage.

### SYNOPSIS

```
du [-abcKLsxDSlX] [--all] [--total] [--count-links] [--summarize] [--bytes] [--kilobytes] [--one-file-system] [--separate-dirs] [--dereference] [--dereference-args] [--help] [--version] [filename...]
```

### DESCRIPTION

This documentation is no longer being maintained and may be inaccurate or incomplete. The Texinfo documentation is now the authoritative source. This manual page documents the GNU version of du. du displays the amount of disk space used by each argument and for each subdirectory of directory arguments. The space is measured in 1K blocks by default, unless the environment variable POSIXLY_CORRECT is set, in which case 512-byte blocks are used.

### OPTIONS

- **-a**, --all: Display counts for all files, not just directories.
- **-b**, --bytes: Print sizes in bytes.
- **-c**, --total: Write a grand total of all of the arguments after all arguments have been processed. This can be used to find out the disk usage of a directory, with some files excluded.
- **-k**, --kilobytes: Print sizes in kilobytes. This overrides the environment variable POSIXLY_CORRECT.
- **-l**, --count-links: Count the size of all files, even if they have appeared already in another hard link.
- **-s**, --summarize: Display only a total for each argument.
- **-x**, --one-file-system: Skip directories that are on different filesystems from the one that the argument being processed is on.
- **-D**, --dereference-args: Dereference symbolic links that are command line arguments. Does not affect other symbolic links. This is helpful for finding out the disk usage of directories like /usr/tmp where they are symbolic links.
- **-L**, --dereference: Dereference symbolic links (show the disk space used by the file or directory that the link points to instead of the space used by the link).
- **-S**, --separate-dirs: Count the size of each directory separately, not including the sizes of subdirectories.
- **--help**: Print a usage message on standard output and exit successfully.
- **--version**: Print version information on standard output then exit successfully.

### BUGS

On BSD systems, **du** reports sizes that are half the correct values for files that are NFS-mounted from HP-UX systems. On HP-UX systems, it reports sizes that are twice the correct values for files that are NFS-mounted from BSD systems. This is due to a flaw in HP-UX; it also affects the HP-UX **du** program.

## EJECT(1)

### NAME

**eject**: Eject removable media.

### SYNOPSIS

eject -h
eject [-f][-u][-v]
eject [-f][-u][-v] <nickname>
eject [-f][-u][-v] <device-name>
eject -d
eject -n
eject -a on | 1 | off | 0 [-v]
eject -c <slot> [-v]

### DESCRIPTION

**eject** allows removable media (typically a CD-ROM, floppy disk, or Iomega Jaz or Zip disk) to be ejected under software control. The command can also control some multi-disc CD-ROM changers and the auto-eject feature supported by some devices.

If no device is specified, a default device is used. The environment variable CDROM can be used to set the default device, otherwise the compiled in default is used.

Other devices can be specified either using the full device name (e.g. /dev/cdrom) or a nickname.

### COMMAND-LINE OPTIONS

- **-h**: This option causes eject to display a brief description of the command options.
- **-f**: Normally eject will not eject a device if it has determined that the device is being used for a mounted file system. This option overrides that behaviour, and attempts to force an eject even for a mounted device.
- **-u**: This option instructs eject to first try to unmount the device before ejecting it.
- **-v**: This makes eject run in verbose mode; more information is displayed about what the command is doing.
- **-d**: If invoked with this option, eject lists the default device.
- **-n**: If this option is used, eject will list the supported nick-names and corresponding devices.
- **-a on | off | 0**: This option controls the auto-eject mode, supported by some devices.
- **-c <slot>**: With this option a CD slot can be selected from an ATAPI/IDE CD-ROM changer. Linux 2.0 or higher is required to use this feature. The CD-ROM drive can not be in use (mounted data CD or playing a music CD) for a change request to work. Please also note that the first slot of the changer is referred to as 0, not 1.

### BUGS/LIMITATIONS

**eject** only works with devices that support the CDROMEJECT or FDEJECT ioctl. It also works with the Jazz and Zip drive using normal SCSI commands. Most CD-ROM drives under Linux should work. The only ejectable floppy devices that it has been tested with are Sun workstation drives running Linux on the SPARC platform.

**eject** may not always be able to determine if the device is mounted (e.g. if it has several names). If the device name is a symbolic link, **eject** will follow the link and use the device that it points to. It will also properly check if any partitions of the device you are trying to eject are mounted (which could be the case on the Jazz, Zip, or even a CD-ROM, really).

If the auto-eject feature is enabled, then the drive will always be ejected after running this command, even if it is mounted and the -f option is used. Not all Linux kernel CD-ROM drivers support the auto-eject mode. The nicknames are set when **eject** is compiled.

There is no way to find out the state of the auto-eject mode. You probably shouldn't be able to eject a mounted disc, but most kernel drivers allow it.

The -u option will only succeed in unmounting if the user has privileges to run unmount(8), or **eject** is installed setuid root, and it is not busy.

### AUTHOR

**eject** was written by Jeff Tranter <jeff.tranter@pobox.com> and is released under the conditions of the GNU General Public License. See the file COPYING and notes in the source code for details.

For suggestions and patches, special thanks go out to: Ben Galliard <bgallia@luc.edu>, Dick Streefland, Donnies Barnes <djb@redhat.com>, Doug L. Hoffman <hoffman@cs.unc.edu>, Grant Guenther <grant@torque.net>, Mark Lord <mlord@pobox.com>, Markus Pilzuecker <markus.pilzuecker@rhein-neckar.netsurf.de>

### SEE ALSO

- mount(2), umount(2), mount(8), umount(8)
- `/usr/src/linux/Documentation/cdrom/`

## GREP(1)

### NAME

**grep**, **egrep**, **fgrep**: Print lines matching a pattern.

### SYNOPSIS

```
**grep** [-tAB] num] [-CEFGHbVchiLInqswvxUu] [-e pattern | -f file]  
[--extended-regexp] [--fixed-strings] [--basic-regexp]  
[--regexp=PATTERN] [--file=FILE] [--ignore-case] [--word-regexp]  
[--line-regexp] [--no-messages] [--revert-match]  
[--version] [--help] [--byte-offset] [--line-number] [--with-filename]  
[--no-filename] [--quiet] [--silent] [--files-without-match]  
[--files-with-matches] [--count] [--before-context=NUM]  
[--after-context=NUM] [--context] [-binary] [-unix-byte-offsets]  
files...
```

### DESCRIPTION

**grep** searches the named input *files* (or standard input if no files are named, or the file name - is given) for lines containing a match to the *given pattern*. By default, **grep** prints the matching lines.

There are three major variants of grep, controlled by the following options:

- **-G**, **--basic-regexp**: Interpret *pattern* as a basic regular expression (see below). This is the default.
- **-E**, **--extended-regexp**: Interpret *pattern* as an extended regular expression (see below).
- **-F**, **--fixed-strings**: Interpret *pattern* as a list of fixed strings, separated by newlines, any of which is to be matched.

In addition, two variant programs **egrep** and **fgrep** are available. **egrep** is similar (but not identical) to **grep** **-E**, and is compatible with the historical Unix **egrep**. **fgrep** is the same as **grep** **-F**.

All variants of grep understand the following options:

- **-num**: Matches will be printed with *num* lines of leading and trailing context. However, **grep** will never print any given line more than once.
- **-A** *num*, **--after-context**=*NUM*: Print *num* lines of trailing context after matching lines.
- **-B** *num*, **--before-context**=*NUM*: Print *num* lines of leading context before matching lines.
- **-C**, **--context**: Equivalent to **-2**.
- **-V**, **--version**: Print the version number of **grep** to standard error. This version number should be included in all bug reports (see below).
- **-b**, **--byte-offset**: Print the byte offset within the input file before each line of output.
- **-c**, **--count**: Suppress normal output; instead print a count of matching lines for each input file. With the **-v**, **--invert-match** option (see below), count non-matching lines.
- **-e** *pattern*, **--regexp**=*PATTERN*: Use *pattern* as the pattern; useful to protect patterns beginning with -.
- **-f** *file*, **--file**=*FILE*: Obtain the pattern from *file*.
- **-h**, **--no-filename**: Suppress the prefixing of filenames on output when multiple files are searched.
