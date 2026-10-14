To see what dd can do on a device, try this:

```
$ dd if=/dev/zero bs=1k count=6 > /tmp/foo
```

While not terribly useful in itself, this command does demonstrate dd’s option structure. This example is as straightforward as it looks: It takes 1-kilobyte blocks of input from /dev/zero (with standard output, the default) into /tmp/foo six times.

dd’s size options are normally specified in bytes, but you can modify this with k (1024 bytes), b (512 bytes), w (2 bytes), and a few other choices described in the info and manual pages. The most important options are:

# bs=n, ibs=n, obs=n

Set block sizes to n. Since there are two block sizes (one for input and one for output), there are three options: bs sets both, ibs sets the input block size, and obs sets the output block size. The default is 512 bytes.

# count=n

Read a maximum of n blocks.

# if=name, of=name

Set the input and output files (the defaults are standard input and output).

# conv=method

This option is mostly for conversion of non-Unix formats. For example, it can convert EBCDIC to ASCII and back (with the ascii and ebcdic methods). See the info page for more details.

Like a number of GNU versions utilities that come with Linux, dd has expanded beyond the versions that come with other Unix variants; the manual page doesn’t list all of the options because GNU wants you to use info documentation. However, dd --help does offer a quick summary.

# cpio

From time to time, you may encounter a cpio archive. This format (or rather, collection of formats) is common on tapes coming from systems such as HPUX and Stardent Titans. The following section covers what you need to know to extract a cpio archive.

cpio has modes, much like tar: extract mode (initiated with -i), create mode (-o), and a pass-through mode (-p) for copying files. Testing an archive is part of the extract mode, and you would input the following:

```
$ cpio -i -t -I archive
```