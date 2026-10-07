You can use `tar` to copy files to tapes or floppies by specifying a device name and the `f` option as a device name. To archive files in `/usr/tparker` to a floppy disk in the first drive, you could use the following command:

```
```
tar cvf /dev/fd0 /usr/tparker
```
```

This can cause a problem if the floppy doesn't have enough capacity, however, so `tar` lets you specify the capacity with the `k` option. In this case, the command for a 1.44MB floppy is as follows:

```
```
tar cvfk /dev/fd0 1440 /usr/tparker
```
```

If the floppy is full before the entire archive has been copied, `tar` prompts you for another one. It's important to keep the arguments in the right order. You see that the `f` is before the `k`, so the device name must be before the capacity. All the argument keyletters are gathered together instead of being issued one at a time followed by their value, which is one aspect of `tar` that can be very confusing.

As a last issue in backing up to floppy, it is sometimes necessary to tell the `tar` program about the blocking used (blocking identifies how many blocks are used for each chunk of information on the device). A floppy usually has a blocking factor of 4, so the command becomes the following:

```
```
tar cvfkb /dev/fd0 1440 4 /usr/tparker
```
```

A final problem with `tar` is that it can't always handle a generic device such as `/dev/fd0` and must be specifically told the disk type.

For more complete information on all the options used by `tar`, check the man pages or, even better, a good system administration book.

You can use `tar` to archive compressed files, too, in the same manner. You can also compress a `tar` file without any problems. In these cases, you might get filenames such as the following:

```
```
fileName.tar.gz
```
```

Filenames such as this show that you should run `gunzip` first to recover the `tar` file, and then run `tar` to extract the files in the archive. You can run the commands together with pipes:

```
```
gunzip fileName.tar.gz | tar xvf -
```
```

The hyphen representing the `tar` filename after the pipe symbol is standard UNIX terminology for taking the input from the pipe (stdin). The `tar` command has a lot of other options, many of which are obsolete or seldom used. We look at `tar` in more detail in Chapter 45, "Backups."