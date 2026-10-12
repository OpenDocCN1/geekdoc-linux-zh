
Yes, this is the home partition. Now change the current directory to Joe's home directory using the cd command. Type ls again to view the contents of his home directory.

```
restore> cd joe
restore> ls
./joe:
.mozilla/                Desktop/                 report.html
.bashrc                  Mail/                    letter.txt
.xinitrc                 News/                    www/
```

Now mark the Mail directory for extraction using the add command:

```
restore> add Mail
```

If you use the ls command again, you see that the Mail directory is preceded with an asterisk (*) character, which means it has been marked for extraction.

```
restore> ls
./joe:
.mozilla/                Desktop/                 report.html
.bashrc                  *Mail/                   letter.txt
.xinitrc                 News/                    www/
```

Now use the extract command to begin the extraction process. restore will prompt you for the number of the tape to start with. This is a single tape backup, so just enter the number 1. When it prompts you to "Set owner/mode for '.'?", answer yes by typing y and pressing Enter. restore will then restore the file permissions (if necessary) of the directory it is restoring to. This isn't critical when extracting individual files like this, but you should always answer yes to this prompt when doing a full restore. Anyway, your screen should now contain the following:

```
restore> extract
You have not read any tapes yet.
Unless you know which volume your file(s) are on you
should start with the last volume and work toward the first.
Specify next volume #: 1
Set owner/mode for '.'? [yn] y
restore>
```

At this point, the files have been recovered and you can exit the restore program by issuing the quit command. That's all there is to it. You now know the basics of using the dump and restore commands.

## Configuring Amanda for network backups

Using Amanda (the Advanced Maryland Automatic Network Disk Archiver), you can use a single large-capacity tape drive on a server to back up files from multiple computers over a network. The Amanda package includes a variety of commands. The online man page for Amanda describes the commands as shown in Table 13-7.

| Command | Description |
| --- | --- |
| amdump | Do automatic Amanda backups. It is normally run by cron on a computer called the tape server host and requests backups of file systems located on backup clients. amdump backs up all disks in the disklist file to tape or, if there is a problem, to a special holding disk. After all backups are done, amdump sends mail reporting failures and successes. |
| amflush | Flush backups from the holding disk to tape. amflush is used after amdump has reported it could not write backups to tape for some reason. When this happens, backups stay in the holding disk. After the tape problem is corrected, run amflush to write backups from the holding disk to the tape. |
| amcleanup | Clean up after an interrupted amdump. This command is only needed if amdump was unable to complete for some reason, usually because the tape server host crashed while amdump was running. |
| amrecover | Provide an interactive interface to browse the Amanda index files and select which tapes to recover files from. amrecover can also run amrestore and the system restore program (such as tar) sometimes. |
| amrestore | Read an Amanda tape, searching for requested backups. amrestore is suitable for everything from interactive restores of single files to a full restore of all partitions on a failed disk. |
| amlabel | Write an Amanda format label onto a tape. All Amanda tapes must be labeled with amlabel. amdump and amflush will not write to an unlabeled tape. |
| amcheck | Verify the correct tape is in the tape drive and that all file systems on all backup client systems are ready to be backed up. Can optionally be run by cron before amdump, so someone will get mail warning that backups will fail unless corrective action is taken. |
| amadmin | Take care of administrative tasks, such as finding out which tapes are needed to restore a file system, forcing hosts to do full backups of selected disks, and looking at schedule balance information. |
| amtape | Take care of tape changer control operations, such as loading particular tapes, ejecting tapes, and scanning the tape rack. |
| amverify | Check Amanda backup tapes for errors (GNU tar format backups only). |
| amrm tape | Delete a tape from the tape list and from the Amanda database. |
| amstatus | Give the status of a running amdump. |

The `amdump` command is the one that you will use the most, but before you can get started, you need to configure a few things on both the backup server (the system with the tape drive) and the backup clients (the systems being backed up).

## Creating Amanda directories

You need to create some directories to hold the Amanda configuration files and to provide a location to write Amanda log files. The configuration files go in an `/etc/amanda` directory, and the log files go in `/var/lib/amanda`. In both cases, you should log in as the amanda user and create subdirectories within those directories, one subdirectory for each backup schedule that you intend to run and an index file, as shown here:

> **NOTE**: For security reasons, you should do all amanda administration as the amanda user. To do this, the root user should create a password for amanda by typing `passwd amanda` and entering the new password. The rest of this procedure assumes that you are logged in as the amanda user.

```
# su - amanda
$ mkdir -p /var/lib/amanda/normal
$ mkdir -p /var/lib/amanda/normal/index
$ mkdir -p /etc/amanda/normal
```

For the purpose of this example, I have created only a `normal` backup configuration that backs up the data drives on several machines. You may also decide to create an `upgrade` backup configuration that backs up the operating system partitions. You could then run that backup before you perform any operating system upgrades.

You also need to specify a holding disk that Amanda can use to temporarily spool backups before it writes them to disk. This directory should have a lot of free space. I have a large `/home` partition on my server, so I created an `Amanda` directory there to use as a holding disk:

```
# mkdir /home/amanda
# chmod 700 /home/amanda
# chown amanda /home/amanda
# chgrp disk /home/amanda
```

## Creating the amanda.conf file

Next, as the amanda user, you must create two configuration files for Amanda and store them in the `/etc/amanda/normal` directory: `amanda.conf` and `disklist`. You can start by copying samples of these files from the `/etc/amanda/DailySet1` directory as follows:

```
$ cd /etc/amanda/DailySet1
$ cp amanda.conf disklist /etc/amanda/normal
```

The `amanda.conf` file sets a variety of general configuration values, and the `disklist` file defines which machines and partitions to back up. The `amanda.conf` file can be rather complicated, but, fortunately, most of its values can be left at their default values. Here is a simplified `amanda.conf` file with some comments embedded in it to help explain things:

```
#
# amanda.conf - sample Amanda configuration file. This started life as
#               the actual config file in use at CS.UMD.EDU.
```

```
org "GLACI"                 # your organization name for reports
mailto "amanda"             # space separated list of operators at your site
dumpuser "amanda"          # the user to run dumps under

# Specify tape device and/or tape changer. If you don't have a tape
# changer, and you don't want to use more than one tape per run of
# amdump, just comment out the definition of tpchanger.

runtapes 1                  # number of tapes to be used in a single
                            # run of amdump
tapedev "/dev/nrft0"        # the no-rewind tape device to be used
rawtapedev "/dev/rft0"      # the raw device to be used (ftape only)

tapetype HP-DAT             # what kind of tape it is
                            # (see tapetypes below)
labelstr "^Normal[0-9][0-9]*$"  # label constraint all
                            # tapes must match

# Specify holding disks. These are used as a temporary
# staging area for dumps before they are written to tape and
# are recommended for most sites.

holdingdisk hd1 {
    comment "main holding disk"
    directory "/home/amanda"  # where the holding disk is
    use 290 Mb               # how much space can we use on it
    chunksize -1             # size of chunk
}

# Note that, although the keyword below is infofile, it is
# only so for historic reasons, since now it is supposed to
# be a directory (unless you have selected some database
# format other than the `text' default)

infofile "/usr/adm/amanda/normal/curinfo"   # database DIRECTORY
logdir   "/usr/sdm/amanda/normal"            # log directory
indexdir "/usr/adm/amanda/normal/index"      # index directory

# tapetypes

# Define the type of tape you use here, and use it in "tapetype"
# above. Some typical types of tapes are included here. The
# tapetype tells amanda how many MB will fit on the tape, how
# big the filemarks are, and how fast the tape device is.

define tapetype HP-DAT {
    comment "DAT tape drives"
    # data provided by Rob Browning <rlb@cs.utexas.edu>
    length 1930 mbytes
```
