
```
config.guess   install-sh   sudo.man
config.h       insults.h    sudo.o
```

This is a directory listing of the source code and object code generated for the sudo command. With this directory listing as our sample, we will answer the following questions using the echo and ls commands to generate the desired output.

- 1. Which of these files begin with the letter "I"?
- 2. Which files in the directory contain the character "y"?
- 3. How would you assign all filenames that end in ".c" or ".h" to a shell variable FOO?
- 4. How would you copy all files starting with "y." to your home directory?
- 5. How would you list all files starting with "visudo." except those ending with a ".c" or ".o" extension?
- 6. How can you list all files starting with the letter "s" and ending with a single character extension?

The first question asks us to list all files beginning with the letter "I". This example will demonstrate the use of the "*" globbing character. To answer this question, we would issue the following command, giving the output shown.

```
[tschenk@quicksilver sudo.v1.5.3]$ ls I*
INSTALL
INSTALL.configure
```

The next question also requires the use of the "*" globbing character. Remember that this character matches zero or more characters, thus the expression "*y*" used in the following command translates to "zero or more characters followed by the letter 'y' followed by zero or more characters." This means that the output will include files that start and end with the letter "y" as well as those that include "y" somewhere in the middle. Here is the command and its output:

```
[tschenk@quicksilver sudo.v1.5.3]$ ls *y*
sixcrypt.exp  lex.yy.o  sudo-lex.yy.c  y.tab.h
lex.yy.c      parse.yacc  y.tab.c  y.tab.o
```

In the next example, we will use the echo command to assign all of the files ending with ".c" or ".h" to a shell environment variable FOO. This will demonstrate the use of the brackets in filename substitution.

```
[tschenk@quicksilver sudo.v1.5.3]$ FOO=`echo *.[ch]`
[tschenk@quicksilver sudo.v1.5.3]$ echo $FOO
allocca.c check.c compat.h config.h doe_pwent.c find_path.c fnmatch.c
getspuid.c getwd.c goodpath.c ins_2001.h ins_classic.h ins_csops.h
ins_goons.h insults.h interfaces.c lex.yy.c logging.c lsearch.c options.h
parse.c pathnames.h putenv.c strdup.c sudo-lex.yy.c sudo.c sudo.h
```

```
sudo_setenv.c testsudoers.c tgetpass.c utime.c version.h visudo.c y.tab.c y.tab.h
(newlines inserted to improve readability)
```

The next example asks us to copy all files starting with "y." to the current user's home directory. This will be accomplished using the "~", or tilde operator. Please note that this expansion will only occur if the "~" character is the first in a string and is followed by a "/" character.

```
[tschenk@quicksilver sudo.v1.5.3]$ ls y.*
y.tab.c y.tab.h y.tab.o
[tschenk@quicksilver sudo.v1.5.3]$ cp y.* ~
[tschenk@quicksilver sudo.v1.5.3]$ ls ~/y.*
/home/tschenk/y.tab.c /home/tschenk/y.tab.h /home/tschenk/y.tab.o
```

Example number five asks us to list all files starting with "visudo." Except those ending with an extension of ".c" or ".o". This is actually trickier than it first appears. Take a look at the following listing and you will see that it actually takes a combination of brackets with the negation operator, the "*" operator, and curly brace expansion to accomplish the desired result.

```
[tschenk@quicksilver sudo.v1.5.3]$ ls visudo.*
visudo.c visudo.cat visudo.man visudo.o visudo.pod

[tschenk@quicksilver sudo.v1.5.3]$ ls visudo.[!co]
ls: visudo.[!co]: No such file or directory

[tschenk@quicksilver sudo.v1.5.3]$ ls visudo.[!co]*
visudo.man visudo.pod

[tschenk@quicksilver sudo.v1.5.3]$ ls visudo.{[!co]*,cat}
visudo.cat visudo.man visudo.pod
```

The final example is a very simple one that demonstrates the use of the "?", or single character wildcard. Take a look at the following to see how we get the desired result of all files starting with the letter "s" and ending in a single character extension.

```
[tschenk@quicksilver sudo.v1.5.3]$ ls s*.?
strdup.c sudo-lex.yy.c sudo.c sudo.h sudo.o
sudo_setenv.c sudo_setenv.o
```

## Power Commands for Power Users

There are hundreds of commands available on Linux systems and the normal user will probably never learn all of them. In fact, most users will learn the minimal set of commands necessary to accomplish their job. This is what separates them from the power users, whose thirst for knowledge will lead them to learn the most effective ways to accomplish any task.

The following set of commands allows the power user to perform tasks that may seem impossible to normal users. At the very least, it simplifies what otherwise is a complex combination of the few basic commands normal users know. This section covers the following commands and gives a few examples of their use:

- find
- awk
- sed

You may look at the list above and think that these commands are not especially powerful. However, the following examples will show that these commands, when used with their plethora of options or in combination with each other, are quite powerful and will let you accomplish tasks that the normal user will marvel at. Let's start with a truly powerful command—the find command.

## find

The find command, as its name implies, is used to find files in a filesystem. In general, the form of the find command is the command name, followed by a path to begin searching, followed by an expression made up of options, tests, and actions. In its simplest form, the find command starts with the current directory and performs the -print action. Here is an example showing this default action.

```
[nia@quicksilver nia]$ find
.
./.Xdefaults
./.bash_logout
./.bash_profile
./.bashrc
./.screenrc
./.bash_history
./.kde
./.kde/share
./.kde/share/applnk
./.kde/share/apps
./.kde/share/apps/kdehelp
./.kde/share/apps/kdisknav
./.kde/share/apps/kfm
./.kde/share/apps/kfm/bookmarks
./.kde/share/apps/kfm/desktop
./.kde/share/apps/kfm/tmp
./.kde/share/apps/kpanel
./.kde/share/apps/kpanel/applnk
./.kde/share/config
./.kde/share/config/desktop0rc
./.kde/share/config/kcmdisplayrc
./.kde/share/config/kfmrc
./.kde/share/config/kpanelrc
./.kde/share/config/kvtrc
./.kde/share/icons
./.kde/share/icons/mini
./.kde/share/mimelnk
./.kderc
./Desktop
./Desktop/.directory
./Desktop/Autostart
./Desktop/Printer.kdelnk
./Desktop/Templates
./Desktop/Templates/Device.kdelnk
./Desktop/Templates/Ftpurl.kdelnk
./Desktop/Templates/MimeType.kdelnk
./Desktop/Templates/Program.kdelnk
./Desktop/Templates/URL.kdelnk
./Desktop/Templates/WWWUrl.kdelnk
./Desktop/Trash
./Desktop/cdrom.kdelnk
./Desktop/floppy.kdelnk
./.xauth
```

Now if this were the only thing that the find command was capable of, it would not be very useful. Table 2.4 takes a look at some of the available options to the find command and what they mean.

TABLE 2.4 Command-Line Options of the find Command

| Option | Meaning |
|---|---|
| -daystart | Calculate times from the start of the day instead of 24 hours ago. Used in conjunction with -atime, -ctime, and -mtime tests. For example, find /tmp -daystart -atime 1 -print will list all files in /tmp accessed since today began. |

## TABLE 2.4 continued

| Option | Meaning |
|---|---|
| -depth | Process the files in a directory before you process the directory itself. This option is useful if the order of processing is important, such as if you were removing all files in a directory and then needed to remove the directory. |
| -follow | Process the file referenced by a symlink, not the symlink. This option might be useful if you were piping the output of the find command to a backup command like tar or afio, where you want to store the actual file and not the symbolic link. |
| -maxdepth N | Descend at most N directory levels below that specified in the path portion of the command line. |
| -mindepth N | Do not apply tests and actions to files at depths less than N. |
| -noleaf | This option turns off an optimization that tells find to assume that there are two fewer subdirectories than the hard link count. This option is needed when searching filesystems that do not adhere to Linux semantics, like MS-DOS filesystems. |
| -xdev, -mount | These two options are synonyms. They direct find to not descend directories on filesystems other than the one containing the starting directory. This is useful when searching by inode, or if you want to exclude network filesystems from your search. |

As you can see, with the appropriate options, the default behavior of find can be altered to provide more utility. In addition to the options listed in Table 2.4, you can specify any number of tests to the files found by the find command. These include tests to check the various times associated with a file, the permissions, owner, file type, and others. For a complete list of the available tests, refer to the find manual page. To see how some of these tests can be useful, let's look at a few examples.

For our first example, we want to find all of the executable files in a directory. To accomplish this, we will use the -maxdepth option to limit our search to the current directory. We'll also use the -perm and the -type tests to specify regular files with any of the executable bits set.

```
[tschenk@nomad ppp]$ ls -l
total 5
-rw------- 1 root daemon 78 Apr 9 22:33 chap-secrets
-rwxr-xr-x 1 root root 265 Sep 16 1997 ip-down*
-rwxr-xr-x 1 root root 349 May 7 1998 ip-up*
-rw-r--r-- 1 root daemon 5 Apr 9 22:33 options
-rw------- 1 root daemon 77 Apr 9 22:33 pap-secrets

[tschenk@nomad ppp]$ find . -perm -111 -type f
./ip-down
./ip-up
```
