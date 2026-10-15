
and exercises. You can also restart it by typing pc-mounttray & as superuser in a console window.

## EXERCISE 16.14

- 1. What is the exact syntax of the Python command that would unmount the USB thumb drive?
- 2. What other file system formats are available, what are their names, and how would you change the commands in Example 16.26 to accommodate those different file formats if they were present on your USB thumb drive?
- 3. After you properly unmount the USB thumb drive, what is in the directory USB? After you unmount it and physically pull the thumb drive out of the computer, does it show up as a device in /dev?
- 4. Try mounting other external USB devices to your file system, such as an Android cell phone, a Nexus 7 tablet, an iPad, an iPhone, an mp3 music player, and so on. What results do you attain? Can any of those devices be mounted as external file systems on your UNIX computer?
- 5. Try mounting an external USB hard drive (usually found in a powered enclosure). We give more instructions on how to do this procedure in Chapter 23.

### 16.4.2.2 Backing up Your Files

We will not go into the general necessity of backing up your files on your UNIX system as a part of maintaining that computer system, because the reasons for that should seem pretty obvious to all users.

According to UNIX system professionals, there is an easy-to-remember and important set of considerations you must make when backing up the system as an ordinary user, and perhaps even as the system administrator. This set of considerations can be posed in simple question form as “How, What, Why, When, Where, and Who?” Some of the answers to these simple questions can be dovetailed together, and we give a selected list of example answers as follows:

> “How” means on a local disk, to Dropbox, to a USB thumb drive manually, to another computer on your home network, automatically by cron, to another hard disk manually, totally, incrementally, to RAID, or any variant and combination of these.

> “What” means just some of your personal files, all of them, only certain kinds of documents, your entire home directory, the whole disk drive, multiple disk drives, and so on.

> “Why” means deciding on the relative importance of “What” you are backing up.

> “When” means hourly, once a day, once a week, once a month, every time you save a particular file, and at what time exactly, like 3 a.m.

> “Where” means very much the same thing as “How”.

> “Who” means you personally, automatically by cron, the designated system administrator, Dropbox.com.

To give you a notion of a prudent strategy to deploy in backing up your own user files, the file that contains the words you are reading right now was archived in the following manner:

- 1. Saved at regular intervals to the hard drive on a local computer
- 2. Saved periodically to a USB thumb drive mounted on that local computer
- 3. Saved periodically to another hard drive on another computer attached to the local area network
- 4. Saved to Dropbox.com

The following examples and procedures in this section assume you have completed Section 16.4.2.1 in preparation for completing the examples presented next. If you are working on a Sun Solaris-family UNIX system, like Solaris, and have not done this example because of the constraints mentioned there, you can still do these examples on your automatically mounted USB thumb drive.

We will use the rsync command to accomplish our backup strategies in this section. This command is similar to cp, except that it is more efficient and faster.

Most importantly, rsync “synchronizes” two files or directory structures so that changes in one are reflected in the rsync duplicate, either locally between drives, or remotely over a local area network (LAN) or the Internet.

It can copy locally or to/from another host over any remote shell, particularly ssh. It has a large number of options that control every aspect of its behavior and permit very flexible specification of the set of files to be copied. The rsync command finds files that need to be transferred using a “quick check” algorithm (by default) that looks for files that have changed in size or in last-modified time. We encourage you to consult the rsync manual page for more information.

The general forms of the rsync command are

Local:

```
rsync [OPTION(S)...] SRC... [DEST]
```

Across a network:

```
Pull: rsync [OPTION(S)...] [USER@]HOST:SRC... [DEST]
Push: rsync [OPTION(S)...] SRC... [USER@]HOST:DEST
```

where OPTION(S) are the valid options for the rsync command, SRC is the source file or directory, and DEST is the destination path.
