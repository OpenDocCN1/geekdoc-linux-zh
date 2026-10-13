
### The Powers of Root
UNIX uses the word root to describe two different concepts. One is the root user, the person with absolute control over everything having to do with the machine. The other is the root directory, one single specific directory on the machine that is considered to be the top of the file system.

You don't need to care what drives are where. Where do other drives appear, if not named by letters or icons? With UNIX, they appear simply as directories located anywhere in the file system. Odd? Not at all. UNIX completely removes the notion of the hardware and the physical location of the files from the concern of the user. This might take a while to get used to, but when you do you'll see that it makes no sense for a user to have to worry about where a file physically resides. If you know its name and where to find it in the file system, why bother worrying about which chunk of oxidized metal (that's what a hard drive is made of, by the way) it lives upon? If you think about it, you'll see that this has other significant benefits. For example, if your system administrator discovers one day that he's run out of disk space to install new software, he can transparently rearrange disks and files. He can move everything out of some overloaded directory onto a new disk and mount the new disk so that it appears in the same place as the old directory—and you'll never know the difference.

### Mounting a drive
The process of telling the file system that the drive exists and at what directory it will appear. On most variations of UNIX, normal users can't mount drives. If you happen to be on a system which enables normal users to mount drives, you need to see your system administrator to find out which drives you can mount, and how to mount them.

*As a matter of fact, you don't even need to care what state your files live in. Another benefit of this abstraction is that your system administrator can cause files, directories, or drives which are physically located on distant machines to transparently appear as part of the file system on your machine. The only difference you might notice in accessing remotely-located files might be a slight slowdown due to the network. So, what does this mean? If your system is set up properly, no matter where you are or what machine you sit in front of, whether you're at your main office or halfway around the world, all your files appear in the same place and all your software is where you always expect it to be.*

*Even if you don't care where your files are, you're always somewhere.* UNIX bases most of its notion of the user environment on the user "being somewhere" located and working in some particular directory. With the advent of new graphical desktop environment tools this is becoming less of a universal concept, but is still a good idea to keep in mind when working with UNIX.

*UNIX commands and filenames are case sensitive.* For both the Windows and Macintosh user, this might come as quite a surprise: UNIX is quite literal in its interpretation of what you type. MyFile doesn't look identical to myfile on paper, and it's not identical to UNIX either. Always note the case of filenames or commands that you are trying to use. Believe it or not, Mail and mail are two different commands, both of which are available on many UNIX variants—and they do two different things!

*Files have three attributes.* UNIX has a very simple idea of file attributes—files can be readable or not readable, writable or not writable, and executable or not executable. Any combination of these options is possible, though some combinations are not particularly sensible. Generally, programs will be readable and executable, and data files will be readable and possibly writable. UNIX, however, takes you at your word. If you tell it that a data file is executable, for instance, it happily gives you the chance to try to run your Rolodex file—which is unlikely to work; if you tell it that a program is writable it just as happily enables you to edit your word-processor—which is likely to make the software useless.

*Everything belongs to somebody.* Every file and directory in the UNIX file system carries around with it information detailing who owns it. The owner of a file can allow or disallow access to a file for other users or other groups of users, and can control whether the file is executable, readable, or writable.

Now that you understand a bit about what your commands are going to be talking to, you can start learning what you need to know to get around.

## NAVIGATING THE FILE SYSTEM
The most basic commands for dealing with the UNIX file system are the ones for moving between directories and finding out what files are in them. Before moving between them though, it’s a good idea to know where you are.

## WHERE ARE YOU? pwd
The pwd (present working directory) command asks your machine to tell you what directory you’re currently in. Any time you’re running a command line, it’s somewhere in the file system—type pwd and it tells you where.

For example:
```
> pwd
/priv/home/ray/public_html/
```

### Path Particulars
/priv/home/ray/public_html/ is a path. The simplest explanation of a path is the shortest set of directories through which you must travel from the root directory to get to the current file or directory. Each directory in the path is separated by a /.

## THE HOME DIRECTORY
To each user, one particular directory is special. This is your home directory. From the standpoint of navigating around the file system, this directory is identical to any other; however, it is significant in that when you log on, it is where you will initially be. You can expect that anything in or below your home directory belongs only to you. To make your life easier, UNIX doesn’t require you to remember the path to your home directory. Instead, it allows you to refer to your home directory simply as ~, and to anybody else’s home directory as ~username.

Now that you know where you are, the next thing you might want to know is what files are with you.

## LISTING FILES
Actually, with UNIX you can list the files just about anywhere, with the exception of places that you don't have permission (more on permissions in Lesson 19, "Permissions"); the easiest place to list files from, though, is "here"—wherever that currently happens to be.

## LS
The ls command lists files. Issued without arguments, ls lists the files and subdirectories in the current directory (the same one pwd would tell you about). For example
```
> pwd
/priv/home/ray/public_html/
> ls
cgi_bin          test.html
images           vral
index.html
```

The preceding example shows that your current directory path is /priv/home/ray/public_html and that this directory contains five things. You can't tell from this listing, but cgi_bin, images, and vral are directories, whereas index.html and test.html are files.

### Covering the Bases
You didn't really have to issue the pwd command to make use of the ls command in the preceding example. It's been included for the sake of clarity. If you already know where you are in the file system, there's no reason to ask the computer to repeat it for you.

If you'd like to list the files in some directory other than the current directory, such as the files in the root directory, you can issue the ls command with a directory option:
- 1. Determine the name of the directory you want to list.
- 2. Issue the ls command as: ls <directory name>.

If you wanted to list the contents of the root directory /, you would type:
```
> ls /
CDROM          lib
bin            priv
core           tmp
dev            vmunix
etc            usr
include        var
```

Everything here except for vmunix, which is the piece of software at the heart of UNIX, and core, which is an error file that really should be thrown away, are directories.

### Filename Facts
Remember that UNIX filenames, and consequently commands, are case-sensitive. UNIX alphabetizes the capitals before the lowercase. This is why CDROM appears before bin.

How can you tell that they are directories? Use option ls to ask it for more information in the listing, specifically the "long" option.

Issue the command as: ls -l <directory name>.
```
> ls -l /
 total 14
dr-xr-xr-x 2 root 512 Jan 8 1995 CDROM
lrwxrwxr-x 1 root 7 Dec 7 1994 bin -> /usr/bin
-r--r--r-- 1 root 8503728 Oct 25 20:16 core
drwxr-xr-x 3 root 11264 Nov 7 13:02 dev
drwxr-xr-x 11 root 3072 Nov 7 13:01 etc
drwxr-xr-x 46 root 2560 Jan 11 1995 include
drwxr-xr-x 23 root 4096 Oct 13 16:29 lib
drwxr-xr-x 4 root 512 Jul 4 1997 priv
drwxrwxrwx 3 root 512 Nov 24 00:30 tmp
-rwxr-xr-x 1 root 1382769 Aug 12 12:57 vmunix
drwxr-xr-x 29 root 1024 Oct 27 17:53 usr
lrwxrwxr-x 1 root 8 May 21 1995 var -> /usr/var
```
