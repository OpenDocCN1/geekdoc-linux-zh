
## Evaluating Backup Software

Like everything else, there’s no one way to decide if any particular backup software package is right for you until after you’ve used it for a while. Hopefully, if it isn’t right for you for one reason or another, you won’t lose any data. You don’t want to have to tell someone that the files are safely backed up, but the only program in the world that can get the data back out again is not available because the only copy you have of that program is on the tape. Or, that when you tried to back up the files, the program destroyed the original data and then saved that corrupted version, so that’s all you can give back.

There are some things that you should look for in backup software, though. Number one on the list is reliability. A backup program that periodically fails is worse than useless, because you don’t have your backups when you think you do. If the buggy program corrupted the original data that you wanted to back up before any backup could be made, you will not be popular with anyone, including yourself. How do you tell if a backup program is reliable? The absolute best way is to use it for a period of time on data that you can afford to lose. For what period of time should you test backup software? If your data keeps growing at a great rate, that probation period may never end, although you should have a pretty good idea after the end of your second time through the rotation schedule. Another means of evaluating backup software is to talk to people who are currently using it, before you commit yourself.

If the software is proprietary, the salespeople should be able to put you in contact with whomever they think you should talk to—probably a happy customer. Find out if that customer has the same (or similar) needs as you in terms of numbers of files and storage requirements. The downside is that you will probably not get to talk to unhappy customers about what some of the drawbacks to the program are. Don’t kid yourself, all software has some drawbacks. The trick is to pick drawbacks that you can live with, once you know what they are.

Open source software, on the other hand, typically has a mailing list that you can subscribe to before you commit. Some have separate mailing lists for users and developers; others have just one list. In either event, the authors are often active participants. Both the good and the bad are typical topics of discussion.

With a proprietary package, the chances are that you will never know who wrote it, or be able to ask technical questions about the program itself. Open source software allows anyone the opportunity to examine the code for potential problems.

The rest of the list of things to look for in backup software will vary from one person to the next. If you are trying to back up several hundred thousand files occupying hundreds of gigabytes every day, your needs will not be the same as if you were concerned with only tens or hundreds of files.

You should look at ease of use. Will this software require a highly skilled person to set it up? Can this software be run by existing staff right now, or will special training be required in order to get it to do what you want?

There may also be issues of compatibility with existing archives of backed up software. If you move from a tar-based system to a proprietary format, and then back again, what happens to the proprietary-format archives if you need to get at something inside?

How easily is the software obtained? If you use a specific program to back up your systems and you add a different operating system to your network, will that software support it? If it isn't supported directly, are you able to support it indirectly? For example, can you easily back up a non-local, NFS mounted directory? How would you restore those files?

## A Backup Software Evaluation Sample

As an example of how I would evaluate backup software, let's consider the program taper. taper is distributed with Red Hat Linux, and was written by Yusuf Nagree. The home page is located at http://www.jugos.si/delo/taper/index.html. The installation program lists it under applications/backup. It installs quite easily. When run for the first time, it responds with a rather cryptic message:

```
[root@clarence /root]# /usr/sbin/taper
Set tape drive using -T option
```

A quick reading of the documentation located in /usr/doc/taper-6.9 reveals a great deal of information. (As a system administrator, you will read a great deal of documentation. Or you will destroy your system often. The choice is yours. I highly recommend reading the docs. RTFM is a standard answer from a system administrator. It could stand for Read The FAQ and Manual. FAQ stands for Frequently Asked Questions. Mailing lists, Usenet groups, and application home pages often have a FAQ available where common answers for common questions are answered.)

The program is considered by the author to be Beta because he only knows that it works on his system. It worked just fine on the floppy-tape equipped machine that I tried it on.

It was written with a floppy-controller tape drive in mind because the author only has one of those. I suspect that using this program on a SCSI tape device would pose no problems, but I would need to test it before I was sure. I'm a system administrator—paranoia is a prerequisite!

The -T option is for specifying which kind of tape drive is attached to this computer. The list given includes SCSI as well as the floppy-controller devices, IDE drives, floppy disks, and files.

There is a limit of about 30,000 files unless you have a large amount of physical memory. Without looking at the sources, which are available, I'm not sure how much a large amount is. Backing up a complete Red Hat install would require in excess of 130,000 files.

Once a tape device (or a file) is specified, taper is controlled via text-based menus.

taper needs to know where the backups will be kept, and where to keep its index files. The first thing that you want to do is set up your preferences—things such as the storage medium (the program supports tape, file, disk, and networked media, according to the docs). You are able to specify the size of the backup devices, which is needed, for example, if you use 40Mb tapes and need to back up 50Mb of data. If you don't remember the keystroke needed for a particular operation, pressing the "?" key brings up a list of keystrokes. Then, select the files or subdirectories that you want backed up (with "s"), and when you are done, the "f" key starts things rolling. It's fast and it appears to be reliable. It will automatically skip the /proc subdirectory.

In order to restore files onto another computer, the index files as well as the program have to be moved there. There wasn't a man page installed, but the documentation in /usr/doc/taper-6.9 is very clear. It allows for unattended full and incremental backups (via cron), and the index is fully browsable within the program so that you can recover specific files.

A major drawback, from my point of view, is that the data appears to be stored in a format that is only understood by taper, and that this format has been changed from earlier versions. I have machines on my internal network that are never updated, for the reason that they accomplish their tasks quite adequately as they are. Because they are on an internal, private network, security is not an issue.

My conclusion: This is not the program of choice for me. I require portable backup files—they may be restored onto any of a number of machines. It may be the perfect backup program for you, or not. If not, then check out another—perhaps kdat is the backup program for you.

## kdat

kdat is another backup program that also ships with Red Hat Linux (it would be installed if you installed the KDE window manager). It can be found under KDE menus, Utilities, Tape Backup Tool. It doesn't work with remote tape drives, which is one of my prerequisites. It does, however, use standard tar commands to save to tape. It has been designed to be a graphical front end to use the tar program and a local tape drive. It does not meet my requirements because I have several machines to back up onto the one tape unit, but it just may be the exact thing that you are looking for.
