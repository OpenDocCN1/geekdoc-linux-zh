
## Chapter 10

What about applications and tools? You probably don’t need to back up your applications, since you can reinstall them from your purchased media or from an online repository. The key here, however, is that you need to keep track of what applications you installed in this manner. The best way to do this is to install them initially into an isolated directory, such as `/usr/local/apps`, and keep the configurations for those applications in `/usr/local/apps/etc`. That way, you can archive each application’s configuration and data files separately.

Finally, what about personal data? Well, that’s simple – we really should archive personal data, because it is likely to be very difficult (if not almost impossible) to re-create that data if we were to lose it.

## Frequency of Backups

Having considered *what* to archive, you now need to think about *how often* you need to perform backups. The answer to this question depends on how dynamic your data is. If your data changes frequently, then you need to archive it on a regular basis to ensure that you can recover the latest versions of the data if something does go wrong.

Don’t worry: frequent backups don’t necessarily have to consume a lot of space, since most backup applications support **incremental backups**. An incremental backup is different to a full or complete backup, in that it archives only those files that have been added or modified since the last full backup.

## Location of Archives

In addition to considering the optimum frequency of backups, you also need to consider how frequently you anticipate having to *restore* files from backup archives. This issue has a big impact on where you decide to archive your data – that is, the media you choose for storing your backups.

For example, do you find that you need older versions of your files on a regular basis? If so, you need to make sure that you back up your data onto a medium that supports fast random access, such as hard disks or network attached storage (NAS).

There are various types of media available for storing archived data, everything from floppy disks and magnetic tapes to CD-ROM, DVD, and hard disks. Here is a table that illustrates some of the advantages and disadvantages of each type of media:

| Media | Advantage | Disadvantage |
| :--- | :--- | :--- |
| Floppy disk | Convenient, Inexpensive, Supported by all operating systems, Suitable for storing configuration files | Limited size: 1.44MB, Slow, Unreliable; prone to damage |
| Removable disks (Zip, USB Flash) | Convenient | Low capacity, Not supported on all operating systems, More expensive than floppy disks, Somewhat reliable |
| Magnetic tapes | Inexpensive, High capacity; ideal for unattended backups | Sensitive to heat and electromagnetic fields, Relatively slow |
| CD-ROM, DVD | Inexpensive<br>DVD has high capacity<br>Reasonably fast | CD-ROM has low capacity |
| Hard Disk | Very fast<br>No media to load<br>Relatively inexpensive | Stored in the same system, which can be a liability |

Keeping all of these ideas in mind, you need to decide how you will proceed to implement an efficient backup and archival strategy.

## Applications and Tools for Archiving

We will now look at several applications and tools, each of which is suited for a different purpose. Let's start with the most basic application, one that is available on almost all Unix platforms, and that is tar.

## Tape Archive (tar)

**Tape Archive**, or **tar**, is a traditional Unix tool for archiving and distributing files. It is best suited to single-user systems and systems with small amounts of data, since it lacks the sophisticated features of more complex backup applications. For example, it has very primitive support for the notion of incremental backups, since it was not designed for that purpose.

tar works by taking a specified set of files and serializing them into one big stream that consists of the **file headers** (name, owner, file creation date) and **contents**. We can store this data stream in a file on a filesystem or store it directly on a magnetic tape.

### Creating a tar Archive

Let's start with a simple example:

```bash
$ tar -cf etc-20020110.tar /etc
```

This will recursively iterate through all the files and subdirectories within /etc and create a tar archive named etc-20020110.tar in the /data/backup directory. The -c option asks tar to create an archive, while the -f option specifies the file to archive to.

What if you want to see the files that tar is archiving? Simple, add a -v (verbose) switch to the command above, like so:

```bash
$ tar -cvf etc-20020110.tar /etc
tar: Removing leading `/` from member names
etc/
/etc/sysconfig/
/etc/sysconfig/network-scripts/
/etc/sysconfig/network-scripts/ifup-aliases
/etc/sysconfig/network-scripts/ifcfg-lo
...
```

As tar archives each file, you will see it listed on your screen. You can use the -v switch with any other option to see verbose output.

### Restoring from a tar Archive

Now, how do we restore files from a tar archive? You can simply do the following (we looked at this in Chapter 3, as well, you may remember):

```bash
$ tar -zvf etc-20020110.tar
etc/
/etc/sysconfig/
/etc/sysconfig/network-scripts/
/etc/sysconfig/network-scripts/ifup-aliases
/etc/sysconfig/network-scripts/ifcfg-lo
...
```

tar will create a directory called etc in your current working directory, along with all the files and subdirectories that were archived. If you don't want to extract all the files, or are not sure what files are contained in an archive, use the -tf switches first to look at the files in the archive:

```bash
$ tar -tvf etc-20020110.tar
```

Then, you can extract a particular file, like so:

```bash
$ tar -f etc-20020110.tar -x etc/sysconfig/network-scripts/ifcfg-lo
```

### Other tar Facilities

tar has other options, such as the ability to **compress** archives, to **include** files from multiple directories, and to **exclude** certain files. Here is another example:

```bash
$ tar -czvf config-20020110.tar.gz /etc /usr /local/apps/etc
```

Here, *tar* will include files from both `/etc` and `/usr/local/apps/etc` into a *gzip* compressed archive, `config-20020110.tar.gz`. You can restore this by using the *-z* switch again:

```bash
$ tar -zxvf config-20020110.tar.gz
```

### Archiving onto Tape

Now, how do we archive files onto tape? On Linux, the expression `/dev/[n]st[n]x` points to the tape device, where the first *n* specifies ‘no rewind’, the second *n* indicates the device number, and *x* specifies the tape density:

| | |
|---|---|
| **L** | **low density** |
| M | medium density |
| a | autoselect density |
| None | default density |

Let’s look at an example where we archive to tape:

```bash
$ tar -cvf /dev/nst0 /etc
```

Typically, a symbolic link `/dev/tape` points to the default tape device.

### Incremental tar Archives

And finally, how do we create incremental *tar* archives that contain files that have been added or modified only since a specific date? Lucky for us, the newer versions of *tar* have an *-N* option which allows us to do this:

```bash
$ tar -cvf etc-20020112.tar /etc -N 01/12/03
```

This will archive files that have been added or modified after 01/12/03.

As you can see, *tar* is a very flexible and powerful archival tool, but one that is not designed to archive arbitrary files located in various directories throughout the system. For that purpose, we use the *cpio* application.

## Archiving with cpio

Early versions of *tar* had its share of limitations. For example:

- It could not create archives that spanned multiple (tape) volumes.
- It could not handle all types of files.
- It could not compress the archives on-the-fly.
- It could not handle bad areas on a tape.

Over time, tar has improved greatly – to a point where these issues are no longer relevant. However, the limitations of early versions of tar were also the motivation behind the development of the cpio archiving tool.

### Creating a cpio Archive

Let's look at an example of cpio in action:

```bash
$ find /etc -print | cpio -vo > etc-20020110.cpio
cpio: /etc: truncating inode number
/etc
cpio: /etc/sysconfig: truncating inode number
/etc/sysconfig
cpio: /etc/sysconfig/network-scripts: truncating inode number
/etc/sysconfig/network-scripts
cpio: /etc/sysconfig/network-scripts/ifup-aliases: truncating inode number
/etc/sysconfig/network-scripts/ifup-aliases
cpio: /etc/sysconfig/network-scripts/ifcfg-lo: truncating inode number
/etc/sysconfig/network-scripts/ifcfg-lo
...
```

We use the find command to get a list of all the files and subdirectories in /etc, and we pass them to the cpio command, which creates the archive on our file system. The -o switch asks cpio to create the archive, while the -v (verbose) switch gives us verbose output (just as it did for the tar command).

### Creating a cpio Archive on Tape

If you want to create the archive on tape, you would simply redirect the output from cpio directly to the tape device, like so:

```bash
$ find /etc -print | cpio -vo > /dev/nst0
```

### Selective Archiving

As you can see, passing filenames in this manner to cpio allows us great flexibility in selecting what files to archive and what not to archive. For example, take a look at this:

```bash
$ find /home/joe -name '*.p[lm]' -print | cpio -vo > pl.cpio
/home/joe/bin/ckmail.pl
cpio: /home/joe/lib/CGI/Lite.pm: truncating inode number
/home/joe/lib/CGI/Lite.pm
cpio: /home/joe/lib/Tie/Handle.pm: truncating inode number
/home/joe/lib/Tie/Handle.pm
...
```
