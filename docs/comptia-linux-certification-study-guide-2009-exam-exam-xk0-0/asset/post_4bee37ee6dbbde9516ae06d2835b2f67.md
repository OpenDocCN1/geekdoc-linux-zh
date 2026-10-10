
enough – just make a copy of stuff you don’t want to lose – but a thorough backup system is incredibly complicated.

There are a number of things to keep in mind when working with backups, including the following:

- What to back up? What information would you miss if something happened to your computer? A much tougher question is “what information would your *users* miss if something happened to *their* computer?” Remember that you may need to restore not just data files, but the entire system, potentially including drive types, partitioning and redundant array of inexpensive disks (RAID) information, and database structure.
- Where to back it up? You’ll want your information squirreled away someplace safe from fire, theft, and natural disasters, but conveniently at hand for quick restores. Two copies may be necessary – one local and one off-site.
- When to back it up? More frequent backups require more resources, but any data accumulated between backups is at risk.
- What to do with all the copies of your information? It needs to be cataloged in some manner, so you can quickly retrieve and restore exactly the file you want.
- Don’t *forget* that even though it’s called *a backup system*, it’s the *restore* that is the point of the entire thing. You need to create and review logs to make sure the backups are really happening, and frequently do test restores of not just files but an occasional entire system so that you know everything works the way it should, and so that you’ll be familiar with how to do it when operating in full-crisis mode.

Not all backups are the same. There are two general kinds of backups – *complete backups*, that contain everything that you deem worth being able to restore; and *partial backups*, which contain only things that have changed since the most recent complete backup. Partial backups are further divided into *differential* and *incremental*. A *differential backup* will contain *everything* that has changed since the last *complete backup*, where an *incremental backup* copies only everything that has changed since the last *partial* backup. If your data doesn’t change much, incremental backups are a lot faster and use much less space than differential; but to do a full restoration, you’ll need to get the last complete backup and *all* of the incremental backups. If you do differential backups you’ll only need the most recent complete and the most recent differential.

Backups can also be done at different levels. File-level backups run at the operating system level and are convenient for dealing with individual files, but require a working operating system to restore to, and may not work well if the file is in use when you try and copy it. Some software, typically databases and some e-mail systems, offer online and offline backups. An online backup uses the database or e-mail system to read each record or mailbox and make a copy. This works great for being able to restore a single mailbox. An offline backup requires that the software that manages the database or the e-mail system be shut down, and then makes a copy of the entire data structure, more like a file-level backup. This interrupts user access to the system, but results in a backup that is much better for restoring the entire system in one go. It is also possible to do an offline backup of entire drive systems and computers themselves by booting them from an alternate device. This is usually the best method to backup a computer as a whole because everything gets copied without having to skip any files the operating system may need to keep open while it is running, and is frequently the best way to restore an entire system in one go. Depending on the configuration and intelligence of your backup utility, you may end up copying information that really isn’t necessary, like swap space, and it is possible to run into problems if you try and restore an entire system onto new hardware if it differs significantly from the old system.

Next, we’ll review some of the tools used for making backups in Linux.

## Copying Data

A couple tools for making file-level copies of data over a network are rsync and ftpd. By copying over a network, it is possible to easily send your backups to off-site locations, although bandwidth may become an issue.

## rsync

The rsync utility is a little different than the others we discuss here. It doesn’t just copy data, it synchronizes it. If you use rsync on a directory, the other end will be made to be an exact duplicate of the original. Depending on the options used, that can include deleting files that aren’t in the source directory, so it should be used carefully.

One of its greatest strengths is that it can read data in blocks, and only copy the portion of files that have changed, called the delta-transfer. This feature means it won’t copy an entire large file if only a small part of it has been modified, which can really save on bandwidth.

It can be run either using a remote shell such as `ssh` or be configured to run as a service, using its own TCP socket and transport system. Note that using `ssh` takes advantage of its extensive encryption and security features, which other shells such as `rsh` and the native `rsync` daemon don't have. It can also be used locally on a single machine – which, by default, disables the delta-transfer feature.

The *man* page for `rsync` is extensive, and is a good reference when preparing for the exam and for “real life” Linux administration once you have passed the exam. The basic syntax for moving files using `rsync` is displayed in Table 11.2.

There are an astounding number of options available in `rsync`; the *man* page for version 3.0.5 is nearly 2700 lines long. Many of them have very subtle differences and interactions with other features. It may be easiest to start with a demonstration.

If you start with a directory that looks like this:

```
chappel@lavie:~$ ls -l
-rw-r-r-- 1 root root 188 2009-07-01 11:13 rights_test
-rw-rw-r--- 1 chappel chappel 4662 2009-07-01 11:13 rights_test2
-rwxr-xr-x 1 chappel chappel 20 2009-06-18 22:54 test.sh
```

If you then perform a basic `rsync` command, the syntax will look like this:

```
rsync * ./rsync_test
```

### Table 11.2: rsync Command Syntax

| File Operation | rsync Command Syntax |
| :--- | :--- |
| Copy files locally from one directory to another | rsync [OPTION...] SRC... [DEST] |
| Pull files through remote shell | rsync [OPTION...] [USER@]HOST:SRC... [DEST] |
| Push files through remote shell | rsync [OPTION...] SRC... [USER@]HOST:DEST |
| Pull files through rsync daemon (option #1) | rsync [OPTION...] [USER@]HOST::SRC... [DEST] |
| Pull files through rsync daemon (option #2) | rsync [OPTION...] rsync://[USER@]HOST[:PORT]/SRC... [DEST] |
| Push files through rsync daemon (option #1) | rsync [OPTION...] SRC... [USER@]HOST::DEST |
| Push files through rsync daemon (option #2) | rsync [OPTION...] SRC... rsync://[USER@]HOST[:PORT]/DEST |

The default `rsync` command will create a new directory for you, called `rsync_test`, the contents of which will be:

```
chappell@lavie:~/test$ ls -l ./rsync_test
-rw-r-r-- 1 chappell chappell 188 2009-07-01 13:26 rights_test
-rw-r--- 1 chappell chappell 4662 2009-07-01 13:26 rights_test2
-rwxr-r-- 1 chappell chappell 20 2009-07-01 13:26 test.sh
```

Notice that the files were copied, including the permissions, but the owner and group of the first file was changed to the default owner and group of the user invoking the `rsync` command, and the timestamps were all changed to the time that the time and date that the command was run. This wouldn't matter if you are just backing up your own files; but if you are copying a home directory for a number of users and then restored the files back to all be owned by root, you would have a mess. To avoid that, you can use the `-a` option (for archive), which will preserve additional file information, and run the command with root privileges to preserve the ownership:

```
sudo rsync -a * ../rsync_test
```

Using the `-a` option now gives:

```
-rw-r-r-- 1 root root 188 2009-07-01 11:13 rights_test
-rw-rw-r--- 1 chappell chappell 4662 2009-07-01 11:13 rights_test2
-rwxr-xr-x 1 chappell chappell 20 2009-06-18 22:54 test.sh
```

Additional options that may be helpful are as follows:

- `-r` or `--recursive` to copy the contents of subdirectories
- `-v` or `--verbose` to get extra information during the copy
- `-n` or `--dry-run` to not actually do anything, just show what would be done—very helpful if you are moving large amounts of data, or including options to delete files
- `-z` or `--compress` to use compression while transferring files, which can save bandwidth

## File Transfer Protocol

Another common way to transfer files is using FTP. Although not normally used for backups, FTP has been around for a very long time and is well supported. Not that the nearly identical functionality and enhanced security offered by Secure File Transfer Protocol (SFTP) (built on `ssh`—see the “SFTP”
