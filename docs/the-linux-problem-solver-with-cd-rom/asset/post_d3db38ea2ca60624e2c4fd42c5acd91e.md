
To see what dd can do on a device, try this:

```
$ dd if=/dev/zero bs=1k count=6 > /tmp/foo
```

While not terribly useful in itself, this command does demonstrate dd’s option structure. This example is as straightforward as it looks: It takes 1-kilobyte blocks of input from /dev/zero (with standard output, the default) into /tmp/foo six times.

dd’s size options are normally specified in bytes, but you can modify this with k (1024 bytes), b (512 bytes), w (2 bytes), and a few other choices described in the info and manual pages. The most important options are:

### bs=n, ibs=n, obs=n

Set block sizes to n. Since there are two block sizes (one for input and one for output), there are three options: bs sets both, ibs sets the input block size, and obs sets the output block size. The default is 512 bytes.

### count=n

Read a maximum of n blocks.

### if=name, of=name

Set the input and output files (the defaults are standard input and output).

### conv=method

This option is mostly for conversion of non-Unix formats. For example, it can convert EBCDIC to ASCII and back (with the ascii and ebcdic methods). See the info page for more details.

Like a number of GNU versions utilities that come with Linux, dd has expanded beyond the versions that come with other Unix variants; the manual page doesn’t list all of the options because GNU wants you to use info documentation. However, dd --help does offer a quick summary.

## cpio

From time to time, you may encounter a cpio archive. This format (or rather, collection of formats) is common on tapes coming from systems such as HPUX and Stardent Titans. The following section covers what you need to know to extract a cpio archive.

cpio has modes, much like tar: extract mode (initiated with -i), create mode (-o), and a pass-through mode (-p) for copying files. Testing an archive is part of the extract mode, and you would input the following:

```
$ cpio -i -t -I archive
```

where archive is the name of the cpio archive (it can be a tape drive). To extract the archive, run this:

```
$ cpio -i -d -I archive filename(s)
```

Here, filename(s) is optional; this instructs cpio to extract only items matching those names. The -d option creates directories as needed (tar does this automatically). Although GNU cpio tries to detect formats automatically, you may also need one of these options after the -i:

### -b

The default format for cpio depends on the byte order of the machine's architecture. This option swaps the byte order.

### -C n

Use n as the block size of the archive.

### -H name

Use name for the type (format) of cpio archive. Options directly relevant to old cpio archives are bin, crc, hpb in, hpoc, newc, odc, tar, and ustar. Note that these are for the GNU version of cpio; other versions (such as the one that comes with BSD systems) don't support as many archive types, and they use different names.

### -v

Verbose (somewhat like tar's verbose setting).
Relevant man page: cpio (1)

## dump and restore

Alternatives to tar, the dump and restore programs come from older Unix utilities that backed up filesystems by looking at their internal structure on the disk (unlike tar and cpio, which use only information from the kernel's filesystem interface). These programs come with a number of Linux distributions, and though they don't work quite the same way as traditional dump and restore programs, they do share the same file format, so you can use them across platforms.

### Interactive restore

You can use restore in automatic and interactive modes. The interactive mode is more popular:

```
# restore ivf filename
```

where filename is the name of the archive (either a device or a file). The command line above grabs the index information from the front of the archive and throws a new command prompt at you:

restore >

At this prompt, you can run cd, ls, and pwd commands (help offers a short summary). As you navigate the filesystem, use the add command to add a file or directory to the list of files and directories you would like to restore. When you add an item to an extract list, an asterisk (*) appears next to it, and if you choose a directory, restore instantly creates it (along with all of its subdirectories).

When you’re finished selecting files, use the extract command to proceed with the actual restoration of the files. restore asks for a volume; just give it 1, since you probably have only a single-volume archive. It also asks if you wish to set the owner and mode for the . directory. If you say yes to this, the current directory will have the same permissions as the mount point of the original archive. If you’re restoring into a different place from the original file location, you probably want to say no to this.

### Automatic restore

To do an automatic restore, run this:

```
# restore rvf $TAPE file1 file2 ..
```

where file1 file2 .. specify what to restore. If you omit them, you’ll restore the entire archive.

### dump

To back up (dump) a directory, use a command like this:

```
# dump -0 -f filename fs|directory
```

The 0 means it’s a full level 0 dump, filename is the device or file in which to store the archive, and fs or directory is the filesystem or directory to back up. In addition to this information, you may need to provide the -d n and -s n options to specify the density and length of your tape.

We don’t recommend using dump for backups. It’s not flexible enough, especially when you’re backing up multiple disks. GNU tar works fine and addresses the traditional arguments against using tar: GNU tar supports single filesystem backups, multiple volumes, and special/sparse files.

## 8.4 Automated Backups with Amanda

Manual backups can be a pain. You can automate the process somewhat by setting a cron job to back up some stuff every night, but it’s difficult to come
