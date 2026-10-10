
You can then burn a CD archive of the image using the `cdrecord` command (as root) like this:

```bash
# cdrecord -v speed=2 dev=0,1,0 -data home.iso
```

You now have an archive of your home directory. This approach can be used to create an archive of your entire filesystem or parts of your filesystem (as long as it’s under 800–650MB). To achieve even better results and be able to store more files, use compression (discussed later in this chapter under “Using the `gzip` Command").

## Creating a Backup Strategy

Backing up files is a chore. But it is a necessary chore if you want to avoid loss of data. Losing data can cost lots of time and money. Backing up files is, therefore, an essential and potentially litigious chore if you administer a multi-user system. The first obstacle to place in the face of disaster is a good backup plan. Some initial questions you should ask are:

- Can the system be administered remotely?
- Does data have to be backed up seven days a week or 24 hours a day?
- Have any current backup strategies been tested?
- How far back (in time) do users need access to the system's data?
- (i.e., can data that is two years old be archived and removed?)
- How many users need to access the data?
- How many redundant systems (power supplies, hard drives, CPUs, etc.) are available?
- How much data needs to be backed up?
- How often is the system upgraded with new hardware or software?
- Is the data in one large file or database, or does it consist of user directories and lots of files?
- Is there a need for off-site storage of the data?
- What are some security concerns about the data? In other words, how sensitive is the data?
- What are the capabilities of the current back up hardware and media?
- What are the storage requirements for the system?
- What is the budget for new hardware or software for back up operations?
- What is the minimum acceptable loss of data (if any)?
- What is the shortest amount of downtime (if any) permitted for the system?
- What kind of back up equipment is already on hand?
- What procedure is currently in place?
- When was the last archive made of the system?
- When was the last backup made of the system?
- When was the last system failure and what caused it?

Obviously no one ever wants to ever lose data: a single document, program, or multimedia file. Is this always possible? The answer is yes, if you take all the necessary precautions, devise a good back up plan, and have adequate equipment. Fortunately, since you use Linux, you also have the necessary software tools.

Some hardware solutions, such as RAID (*Redundant Array of Inexpensive Disks*), can provide an initial measure of security, but it is best to devise a schedule that can cover any loss of data and still have a backup in place. For example, an incremental backup strategy is extremely beneficial and can shorten the time required for back-ups, as the operation saves only those files that have changed since the last backup.

One approach, using two sets of media is:

- **Sunday.** Back up the entire system
- **Monday through Saturday.** Back up all changed files

Another approach, requiring seven sets of media is:

- **Sunday.** Back up entire system
- **Monday through Saturday.** Back up all changed files from the previous day

Yet another more comprehensive approach is:

- **Sunday.** Back up the entire system
- **Monday through Saturday.** Back up all files changed from the previous day
- **Following Sunday.** Backup all files changed from previous week
- **Following three weeks.** Backups are repeated and the process is started over

Choosing an economical backup medium can also be a crucial factor. However, due to the low prices of CD-Rs, high-speed and high capacity tape drives, and the continual dropping cost of hard drive storage, many administrators are choosing one of these media.

### Using the gzip Command

The GNU `gzip` command is a compression and decompression utility similar to Stuffit. However, `gzip` does not have the ability to save the resource fork used by Mac OS files. *gzip* may be used on text or binary files, but it will only recognize the data fork of Mac OS files.

The *gzip* command is used to compress and decompress file and directories. You can use this command to make extra room on a crowded filesystem, or create archives of entire directories. In some cases, especially with text documents, compression ratios can be better than 2:1.

> Another compression utility included with most Linux distributions is the *bzip2* command, which performs even better compression than *gzip*. However, *gzip* compression remains quite popular, has proven to be robust, and is even part of other compression commands, such as the *archive* command **tar**, **zcat**, and **zless** pagers.

![](img/1ea833f5a3e3c1547e3dd2891f52804a_431_0.png)

Using *gzip* is easy. For example, to compress a file, use *gzip* like this:

```bash
$ **gzip -v** usingthezshell.msg
usingthezshell.msg  67.6% -- replaced with usingthezshell.msg.gz
```

The *v* or *verbose* option prints the percentage of compression and the resulting filename. You can also recursively compress an entire directory using this command. For example, as root:

```bash
# **du -b --summarize /usr/share/doc/howto**
51425280		/usr/share/doc/howto
# **gzip -r** /usr/share/doc/howto
# **du -b --summarize /usr/share/doc/howto**
27000832		/usr/share/doc/howto
```

In this example, the contents of the */usr/share/doc/howto* directory require more than 50MB of hard drive space. Following compression with the *gzip* command, the directory requires less than 28MB, a savings of more than 22MB for the directory. (Of course you can save even more room by removing the HOWTOs.)

The *gzip* command may also be used in a shell pipe to compress the standard input. For example, if you create large security logs, you can append compression to the end of the stream like this:

```bash
# **find / -mtime -1 -print -xdev | xargs ls -1 | gzip > /tmp/seclog.gz &**
```

You can use the *gzip* command with its *-d* option to decompress a compressed file. Many Linux users, however, turn to the companion *gunzip* command, because it can handle traditional DOS zip compressed archives such as .zip files and UNIX compress command archives such as .Z files. Use gunzip like this:

```bash
$ gunzip out.gz
gunzip: out already exists; do you wish to overwrite (y or n)? y
```

Note that if a file with the same name as an uncompressed file already exists, you will be asked if you want to overwrite the file. The gunzip command will also decompress files according to a list of files fed in through the standard input. This means that you can easily decompress a list of files, a directory of files, and every file on your system!

Linux includes quite a few compression utilities. You can find quite a few by using the apropos command like this:

```bash
$ apropos compress
```

## Using the tar Command

The tape archive, or GNU tar command is one of the most popular archiving and compression programs in existence. Similar to other compression utilities, such as StuffIt for Mac OS or WinZip for Windows, tar is used by many different Linux distributions and programmers in order to distribute archives of programs, source code, and other documentation.

As a system administrator, you can use the tar command for backup operations by copying users' directories or entire filesystems to removable media, such as tape drives, hard drives, or remote storage devices. By combining the output of the find command with tar's archive building, you can quickly devise software tools to back up your system according to file timestamps, size, or ownership.

For example, to back up all files under the /home directory, you can use tar (as root) like this:

```bash
# tar cvzf /mnt/remotehd/home.tgz /home
```

This command line will create a gzip tape archive named home.tgz under the /mnt/remotehd directory. To only archive files that have changed in the last day, use the find command to feed tar a list of filenames like this:

```bash
# find /home -mtime 1 -print | tar cT - ->mnt/remotehd/home01.tgz
```

In this example, the find command returns a list of all files that have changed in the last 24 hours. This list is piped into the tar command, which then creates a compressed archive of the directory's contents with the name home01.tgz.
