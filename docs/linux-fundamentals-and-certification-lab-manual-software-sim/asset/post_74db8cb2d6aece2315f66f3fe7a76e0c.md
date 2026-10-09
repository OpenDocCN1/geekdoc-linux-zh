
information and access is needed not only during pay periods, but later when completing tax forms and reports.

## Backup Programs Included with Linux Distributions

Backup programs include utilities that are provided with most Linux distributions and third-party programs that must be installed after the Linux installation. Programs that are included are tar, cpio, and dump.

**Using tar** The options you use with tar were listed earlier in this chapter. Basically, to create an archive, you will be using c for create, v for verbose, l (lowercase letter L) for one file system (backs up or restores only one partition), p for same permissions (preserves all protection information), and f to name the archive file to use. For example, to back up the home directory to the tape st0, use the **tar -cvlpf /dev/st0 /home** command.

The option l, also written as --one-file-system, tells tar to back up only files that are in the current file system. Remember that you mount multiple file systems in the same directory hierarchy. Some of the files can physically be on other hard drives or on other computers.

Should a restore become necessary, use the tar extract backups to a tape. This command can be used to extract the entire archive or just some of the files within the archive. For example, to restore the entire *home* directory from /dev/st0, type the **tar -xvlpf /dev/st0 /home** command.

To extract some of the files from the archive, you have to know the exact name of each file or directory to be extracted. If you do not know the name you can use the -t option to get a list of everything in the archive. To extract the directory */home/jsmith* from the /dev/st0 tape drive, use the **tar -xvlpf /dev/st0 /home/jsmith** command.

The tar command also supports an incremental backup option, -g or --listed-incremental. This command provides for incremental backups to a tape.

**Using cpio** The cpio program copies files into or out of a cpio or tar archive. The archive can be a file on a disk, a magnetic tape, or a pipe. The cpio command has three operating modes:

- **Copy-out mode** allows cpio to copy files into an archive. It reads a list of filenames from standard input and writes the archive to standard output. Typically, the **find** command is used to generate the standard input list.
- **Copy-in mode** copies files from an archive to the original file locations. If no file patterns are given, all files are extracted.
- **Copy-pass mode** combines copy-out and copy-in without using an archive. This mode uses a list of files from standard input and copies them to another location.

The **find** command is typically used to produce the standard input for the cpio program. The find command searches the directory tree for a provided expression. Expressions can be paths, devices, the time a file was changed, and many others. Use **man find** to get a more detailed list of find options. Some examples:

- **find /home/** lists all files, using */home/* as a starting point
- **find /home/ -ctime 1** lists all files that were changed one day ago
- **find /home/ -user *uname*** lists all files that belong to the user *uname*

The cpio command has many options in its syntax. To see more options, use the **man cpio** command. The three mode options are:

- -i (copy-in) extracts files from the standard input.
- -o (copy-out) reads the standard input and copies the files onto the standard output.
- -P (copy-pass) reads the standard input.

With the mode command you can also use the following options:

- -a Reset the file access times after they have been copied
- -A Append files to an archive
- -d Create directories as needed
- -I <file> Read the contents of file as an input archive. This is used only with the -i option.
- -v Verbose mode. Prints a list of file names.
- -V Verbose mode, except it prints a dot (.) for each file read or written

The following are examples of combining the find and cpio commands:

To archive all the files from jsmith’s directory to an archive in /root called jsmith_backup.cpio, use the **find /home/jsmith/ | cpio -o > /root/jsmith_backup.cpio** command.

To restore the archive jsmith_backup.cpio in the /root directory to its original directory, use the **cpio -i < /root/jsmith_backup.cpio** command.

## Using dump and restore

The dump and restore programs are carryover programs from Unix. Administrators who are familiar with Unix use these programs because they are familiar and available; however, Linux is not a viable operating system for these older programs. The following is a comment from Linus Torvalds explaining why the use of dump is not advisable.

> **From:** Linus Torvalds <torvalds@transmeta.com>
> **To:** Neil Conway <nconway.list@ukaea.org.uk>
> **Subject:** Re: [PATCH] SMP race in ext2 - metadata corruption.
> **Date:** Fri, 27 Apr 2001 09:59:46 -0700 (PDT)
> **Cc:** Kernel Mailing List <linux-kernel@vger.kernel.org>
>
> [ linux-kernel added back as a cc ]
>
> On Fri, 27 Apr 2001, Neil Conway wrote:
>
> > I’m surprised that dump is deprecated (by you at least :)). What to
> > use instead for backups on machines that can’t unmount disks regularly?
>
> Note that dump simply won’t work reliably at all even in 2.4.x: the buffer cache and the page cache (where all the actual data is) are not coherent. This is only going to get even worse in 2.5.x, when the directories are moved into the page cache as well.
>
> So anybody who depends on “dump” getting backups right is already playing russian roulette with their backups. It’s not at all guaranteed to get the right results—you may end up having stale data in the buffer cache that ends up being “backed up”.
>
> Dump was a stupid program in the first place. Leave it behind.
>
> > I’ve always thought “tar” was a bit undesirable (updates atimes or
> > ctimes for example).
>
> Right now, the cpio/tar/xxx solutions are definitely the best ones, and will work on multiple filesystems (another limitation of “dump”). Whatever problems they have, they are still better than the _guaranteed_(*) data corruptions of “dump”.
>
> However, it may be that in the long run it would be advantageous to have a “filesystem maintenance interface” for doing things like backups and defragmentation.
>
> Linus
>
> (*) Dump may work fine for you a thousand times. But it _will_ fail under the right circumstances. And there is nothing you can do about it.

Given this problem, the use of dump and restore is strongly discouraged.

## Other Backup Programs

Several other backup programs are available that have a lot of nice features that relieve the work load of administrators responsible for making backups. Some will back up multiple machines, use standard software for the actual backup, support tape management, and perform other tasks.

One package that is open source and free is Advanced Maryland Automatic Network Disk Archiver (Amanda). Amanda is suitable for large amounts of data and for network use, and has a client and a server component. The server component runs on a server that typically has a backup device, such as a tape drive. The client component runs on machines that want to use the backup device.

Several commercial backup programs for Linux are available, including UNiBACK (www.orbitisw.com/uniback_for_linux.html), Bru (www.toligroupl.com/), Veritas Backup Exec (www.veritas.com), and BrightStor ARCserve (www3.ca.com/Solutions/Product.asp?ID=3370), to name just a few. Commercial products provide backup and restore features with support. Some of the commercial products are superior to the free programs. If your Linux system is used in a commercial venture, you may want to invest in a product that provides technical support.

## Controlling a Tape Drive

Control a tape drive with the **mt** command. The mt command controls the tape with a given set of options. The syntax of the mt command is **mt -f <device> <operation> [count]**, where device is the device name of the tape (for example, /dev/st0), operation is one of the control commands listed below, and count is an optional value for some commands. Several control commands are used with mt, of which a few are listed here. To see a full set of options, use the **man mt** command.

| Command | Description |
| :--- | :--- |
| **fs <count>** | Move forward count files. |
| **rewind** | Rewind the tape. |
| **offline** | Rewind and unload the tape. |
| **retension** | Rewind the tape and then wind it to the end of the reel, then rewind it again. |
| **erase** | Erase the tape. |
| **status** | Print the status of the tape. |
| **load** | Load the tape. Most tape drives will automatically load when a new cartridge is inserted. |
| **lock** | Lock the tape drive door on SCSI tape drives. |
| **unlock** | Unlock the tape drive door on SCSI tape drives. |

The attached SCSI tape drive type can be found in the file /proc/scsi/scsi (Figure 6-13).

You can use these commands to perform an incremental backup of the /home directory Monday through Thursday; then on Friday, perform a full backup on a new tape. On Monday execute the following set of commands:

```
# Monday's backup
# Rewind the tape
```
