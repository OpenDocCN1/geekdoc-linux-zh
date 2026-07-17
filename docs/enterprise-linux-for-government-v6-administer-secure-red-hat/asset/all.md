![](cover.jpeg)

Enterprise Linux for Government

Administer & Secure
Red Hat Family Linux
version 6

John Timaeus & Russell Overton

![](OEBPS/image_17-resized-399-103.jpg)

Copyright © 2017 JANUS Research Group, Inc
600 Ponder Place Dr, Evans, GA 30809  (706) 364-9100

All rights reserved. No part of this publication may be reproduced, distributed, or transmitted in any form or by any means, including photocopying, recording, or other electronic or mechanical methods, without the prior written permission of the publisher.

Linux is the registered trademark of Linus Torvalds in the U.S. and other countries.

Red Hat, Red Hat Enterprise Linux, Enterprise Linux, Ansible, CentOS, and Fedora are trademarks or registered trademarks of Red Hat, Inc. or its subsidiaries in the United States and other countries.

Oracle, Oracle Linux, and Unbreakable Enterprise Kernel are trademarks of Oracle and/or its affiliates

UNIX is a registered trademark of The Open Group.

The Filesystem Hierarchy Standard is a Copyright of The Filesystem Hierarchy Standard Group, and Daniel Quinlan, Paul Russel, and Christopher Yeoh.   [http://www.pathname.com/fhs/pub/fhs-2.3.html](http://www.pathname.com/fhs/pub/fhs-2.3.html)

The OpenSCAP scap-security-guide is an unlicensed, public domain work of the US Government.
XFS is a trademark of Silicon Graphics International Corp. or its subsidiaries in the United States and/or other countries.

Any other trade names or trademarks are the property of their respective owners.  Neither the authors or JANUS Research Group assert any claim, affiliation, or endorsement with or by any of the above corporations or their intellectual property.

version 1.1-c – April 2018

README.md

About the Book:

This book, and its companion material can be used either for self-study or in a classroom.  While it is specifically tailored for Enterprise Linux version 6 in a US government facility, the principals taught here apply to anyone running any Linux flavor in a security conscious environment.

Enterprise Linux for Government began as a course for database and system administrators supporting the US Army National Guard.  Like many things in the Linux world, a tool developed for a specific niche has found other uses.  The development of a course became the writing of a book. That in turn spawned the JANUS Technical Academy Program, which is now developing courses covering a range of Information Technology subjects.  We anticipate providing a professional certification path for administrators in 2019.  If you have an intrest in becoming a JANUS Certified Linux Administrator, email: academy@janusresearch.com.

JANUS Technical Academy provides training based upon this material, either on-site or remotely.  We can also provide custom course development.  For more information, or if you would like to become an Academic Partner using this course in your classroom, please contact JANUS Research Group.  

Getting Started:

This book is meant to be read with computers nearby, typing as you read.  A full lab setup guide and all requisite scripts and files can be found at
https:// github.com/janustechacademy/EL6.  

A printable copy of the Lab Guide and Command Summary is also available there.  We have found it best to  have them in hard copy  while working.

Authors:

John Timaeus and Russell Overton have been IT administrators, consultants, and instructors since time immemorial.  They are both currently on contract to the National Guard.

Bugs:

We know there are some errors; in a book this size they are inevitable.  As much as we would like to blame others, they are entirely our own.  

To report them: academy@janusresearch.com.

Acknowledgements:

Thanks to all who helped us get through this process.  

Damon Leavit, our course manager, who gave us the inspiration for getting things together in the first place.

David Sales, our boss, who gave us the time and resources to make it happen.

Reno's Argenta Cafe, who kept us fed.

And especially:
April and Amanda, who kept us sane(ish) through it all.
At least we're no crazier than when we began.

Module 0:
Introduction to Linux

What is Linux?

You will work with several computers in this class.  With the possible exception of an access computer, all will be running Linux, a free and open-source software originally developed in 1991.  It is Unix-like but is not UNIX™.  If you have used other UNIX systems you will see many similarities, but you will need to be aware that many things, ranging from the initialization process to the file system hierarchy, are different. 

A Linux operating system is defined by the use of the Linux kernel, or core process.  There are hundreds of variations – known as distributions or 'distros' – that all share the same kernel.  Some have been specialized for use as web servers, firewalls, thermostats, or phones (Android phones run Linux).  We will be using an operating system from the Red Hat Enterprise Linux family.  There are several versions in the Red Hat family that you should be aware of: 

*   Fedora – the free version of Red Hat.  Owned by the Red Hat corporation, but not supported by them.  It has a very quick release cycle and is often more cutting edge than the other versions.  Each release is maintained for only a year or two.  This is not what is meant by Enterprise Linux.
*   Red Hat Enterprise Linux (RHEL)– the not-free version.  Owned and supported by the Red Hat corporation.  You do have to pay for the support.  The maintenance life cycle is guaranteed to be at least 10 years from release.  The release cycle is slower as the point of RHEL is stability.
*   CentOS – another free version.  A direct recompilation of the RHEL source code (which Red Hat must release under the terms of the GNU license).  Some small options may be changed during the compilation, and the Red Hat branding is removed.  There is no option to pay for support through the community.  You will not have access to the Red Hat specific repositories for software, but unless you look at the background, you probably won't be able to tell the difference.
*   Oracle Linux – a custom distribution by Oracle; free to download, but with paid support.  Ships with an alternative proprietary kernel called the Unbreakable Enterprise Kernel, which has some enhancements, mainly in the performance and hardware support areas.

Other distros based on RHEL include ROSA, Scientific Linux, Fermi Linux, SME Server, as well as EulerOS and Inspur K-UX (which do actually qualify as a UNIX™, but that's another story).  As of early 2018, the current version of the Enterprise Linux family is 7.5.  This class is tailored to the latest stable release of the previous version:  Enterprise Linux 6.9, which will be supported through November 2020.  From this point we will simply refer to the operating system as EL6.  If you prefer to read that as Red Hat, CentOS, or Oracle Linux, feel free to do so.

You can determine EL version with cat /etc/redhat-release, for details: uname -a.

Before we can dive into the details of a full operating system we first need to have a little acclimatization in the environment. 

Users and Groups

User accounts are assigned to the individual humans who will ultimately operate in the Linux environment.  Each user should, according to best security practices, be associated with a single user account and it is under this account that most work should be done.  By default, these accounts will exist in a system-local database, but in some environments, they may be stored on a centralized authorization server (LDAP, or Active Directory implementations are examples of this).  When a user account is created, a few basic pieces of information will be recorded.  These are:

*   A username – this is sometimes called a “login name”, “logname”, or “login”.  It is the unique account name which identifies a user on the system.  It might be as simple as a single, lowercase alphabetic string (such as “jsmith”), or it might incorporate other characters (john.smith34).  As with most things on Linux, usernames are case sensitive.
*   A userid – abbreviated as UID, the userid is a number that is used internally by the system for the purposes of identification.  The root account, for example, always has a UID of zero (0).  On most modern Linux systems, userids will be automatically assigned at the time of account creation, and will begin at 501.  As users are added and removed from the system, these numbers may be recycled.  UIDs should be unique to a user account, but in certain circumstances, they can be assigned to multiple accounts.  This is not a secure practice.
*   A password – a password is a secret character string or phrase known only to an individual user, and are designed to provide a form of proof of identity.  Various rules can be implemented to control the complexity, security, and longevity of passwords.  Although accounts can be created without passwords (and in fact, this is the default behavior), users cannot login without a password or similar mechanism.  The account can still own files and be used in other ways beyond the scope of this introduction.  Passwords should never be shared with anyone, for any reason.  Administrators do not require a user’s password, and should never ask for it.
*   A primary group – user accounts can be associated together into groups based on factors such as shared function (sales, accounting, etc.) or by location (office, headquarters), or any other factors an administrator feels are appropriate.  Although user accounts can be assigned to many groups, there will always be a single group, the primary group, which takes precedence.  On an EL6 system, the default primary group for any new user will be a newly created group, named after the login, which will contain only the new user and no others (ex. new user jsmith defaults to a new primary group of jsmith).  As with users, groups also have unique numerical identifiers, which we call Group IDs, or GIDs.
*   A home directory – this is a directory designed to hold user specific files.  For example, the configuration files which control certain parts of a user’s environment will be stored here.  This is also the directory into which a user will be deposited upon successful login.  Users typically have full control over their home directories and the files created inside of them.
*   A shell – we will cover shells more thoroughly in a moment, but for now, understand that these are the programs that receive input from users and allow them to manipulate the operating system.  The simplest way to explain a shell is to say that it is “the thing that you are typing at.”

Taken together, this information defines a user on an EL6 system.

Returning to the concept of groups; groups are an additional point to which permissions may be assigned.  Without groups, we would have difficulty controlling which individuals should have access to files and resources on the system.  Imagine trying to control access to every file, process, and device on a system using only user names.  The access controls would quickly become enormous and difficult to maintain.  Groups provide a way to identify sets of users with similar needs and access requirements, and through their implementation, we can greatly simplify administration of secure systems.

Users will always be assigned to at least one group at account creation – a primary group which is created for them.  Membership in other groups is also possible.  Each of these additional memberships will be referred to as “secondary groups”.

Kernel and Shell

The kernel is the essential engine of the system.  It is tasked with directly manipulating hardware such as processors, memory, and disks, as well as other hardware such as NICs and HBAs.

The kernel is in complete control of the operating system, and will be loaded at boot time into a special, protected area of system memory.  Other programs running on the system operate in an area of memory referred to as “user space”, and will request actions from the kernel using system calls.

Users will not interact directly with the kernel.  Instead, we have specialized programs, called shells, which serve as our command interpreters.  The shell will take our commands and translate them into requests to the kernel for action on our behalf.

In EL6, the default shell is the Bourne Again SHell, or bash.  In a typical login scenario, a user provides his or her username and password to the login program, which then invokes the kernel to start a user’s specified shell and deposit them into a home directory.  When a user logs in, they will see something like this:

[user@host ~]$

This is the shell prompt, or, given the overwhelming prevalence of bash as the default shell, it is often called “the bash prompt”.  It represents the username, the hostname, and the directory currently occupied by the user (also called “Present Working Directory, or PWD).  The dollar sign $ indicates an unprivileged, or non-root, user.  If we had logged in as root (the all- powerful superuser account), we would usually be greeted by this:

[root@host ~]#

The pound sign # indicates the presence of root. 

Directories and Paths

Though a wide array of graphical environments and programs are available in the Linux ecosystem, EL6 is, at its heart, a command line driven operating system.  This means that, from a user’s perspective, the operating system looks something like this:

[root@ELG-6 /]# ls

bin     dev   lab      lib64       misc  opt   sbin     sys  var

boot    etc   lab.tar  lost+found  mnt   proc  selinux  tmp  web

cgroup  home  lib      media       net   root  srv      usr

For new users, this sort of environment can be difficult to comprehend.  We can state, however, that the output above is showing us a list of files and directories.  In the following sections, we will briefly discuss what directories are, and how files and directories are typically structured in EL6.

Much could be written about what directories really are, but for the purposes of this instruction we will treat them as:

*   A series of named containers
*   Organized hierarchically
*   Capable of containing files and other directories

Although administrators are free to create essentially any directory structure they would like, there are certain directories which will either always be present on EL6 systems, or that will be present by default.

We will begin with the root directory, indicated by a forward slash /.

The root directory is similar in function to the root of a tree.  All other directories grow up and out from the root. 

/
  /var
    /var/sub1
         /var/sub1/sub1a
    /var/sub2
  /usr
    /usr/sub1

When other file systems are mounted, they will be mounted to a directory in the root file system.  If we need to describe the location of any file, we may do so by describing the path to it, starting from root (/).  The next section addresses pathing in more detail.

Pathing

The path to any file can be described either from root (called an "absolute path") or from the user’s present working directory (called a "relative path").  Using the directory layout above, the path to the subdirectory sub1a under /var can be described as:

*   Absolute path from anywhere: /var/sub1/sub1a
*   Relative path from /var:  sub1/sub1a
*   Relative path from /var/sub1:  sub1a

Note that the two relative paths in the examples above were NOT preceded by /.  That is because a slash at the start of a path indicates that the path begins at the root directory.  Consider the following command string, which uses cd, the command to “change directories”:

# cd sub1/sub1a.

The effects of this command depend entirely on the user’s current location in the directory structure (Present Working Directory or PWD).  The above command could:

*   Go to /etc/sub1/sub1a (if PWD = /etc)
*   Go to /var/sub1/sub1a (if PWD = /var)
*   Fail (if the PWD did not contain a directory called sub1)

Prepending the slash would make the path look like this: /sub1/sub1a.  This tells the system to start looking in root (/) for a directory called sub1 and then for a sub1a inside of that.   We can see in the earlier structure diagram that such a directory does not exist.  This path is an absolute path, in that it begins from root, but the directions are wrong.  Here’s a working path:

/etc/sub1/sub1a

This path will always take us to the sub1a directory in /etc/sub1, regardless of the user’s PWD when the path was invoked.

There are two special entries that exist in every directory.  These are:

*   .     a dot.  It represents the directory it is inside of.
*   ..   two dots.  These represent the directory above this one.

We can better demonstrate this with a quick example.  The pwd command will return a user’s present working directory.  Let’s make use of it to explore the concept further:

# pwd

/test/1/2

# cd .

# pwd

/test/1/2

Here we have invoked cd in order to change directories to .

Since . is a surrogate for wherever we are, the cd command simply succeeds in putting us where we already were.

# pwd

/test/1/2

# cd ..

# pwd

/test/1

# cd ../../

# pwd

/

Here we used cd .. to move from /test/1/2 to the parent directory /test/1.  We then used cd ../../ to move from /test/1 up two directories to /.

Standard Directories

The Filesystem Hierarchy Standard (FHS) defines a standard set of names, locations, and permissions for many file types and directories in Unix and Linux.  The intent is to provide a consistent working and development environment across distributions.  One would expect, for example, to find configuration files in /etc and device files in /dev regardless of platform.

The information below comes directly from the FHS v2.3:

*   /bin – Essential command binaries
*   /boot – Static files of the boot loader
*   /dev – Device files
*   /etc – Host-specific system configuration
*   /lib – Essential shared libraries and kernel modules
*   /media – Mount point for removeable media
*   /mnt – Mount point for mounting a filesystem temporarily
*   /opt – Add-on application software packages
*   /sbin – Essential system binaries
*   /srv – Data for services provided by this system
*   /tmp – Temporary files
*   /usr – Secondary hierarchy
*   /var – Variable data

Additionally there are several special directories, these do not contain files as such, but expose kernel level information to the user as if they did.  These include:

*   /proc – Contains running processes
*   /cgroup – Control groups which limit resource usage
*   /dev – Physical and virtual devices

Issuing Commands

Working inside of a command line operating environment requires operators to issue syntactically correct instructions.  Linux can be rather unforgiving of improperly formatted instructions, generally resulting in a failure to perform.  More worrisome, perhaps, is the event in which a badly formatted command unfortunately succeeds in doing things which we did not intend.

Command strings in Linux can be broken into three major parts:

*   Command – this is the program we are calling. 
*   Options – these are modifiers that alter the default behavior of a called program.  They will frequently look like this: -ef, -la, -v or this: --line-numbers, --name
*   Argument – This is the target of the command.

These will be separated by whitespace.  In other words, when the shell sees a space in a command string, it assumes that we have finished with our instructions for a section and moved on to another. 

Let’s briefly explore this.  If we call the ls command without options or arguments, it will do this:

# ls

bin     dev   lab      lib64       misc  opt   sbin     sys  var

boot    etc   lab.tar  lost+found  mnt   proc  selinux  tmp  web

cgroup  home  lib      media       net   root  srv      usr

Here, ls has returned a listing of files in the user’s present working directory.  We can alter the behavior of commands by supplying options.  Let’s try using -l (long listing) and -a (show hidden files):

# ls -l -a

total 136

dr-xr-xr-x.  28 root root  4096 Nov  7 14:58 .

dr-xr-xr-x.  28 root root  4096 Nov  7 14:58 ..

-rw-r--r--.   1 root root     0 Nov  7 08:21 .autofsck

dr-xr-xr-x.   2 root root  4096 Nov  7 14:58 bin

dr-xr-xr-x.   5 root root  4096 Sep  7 09:58 boot

drwxr-xr-x.   2 root root  4096 Oct  3 23:52 cgroup

drwx------.   3 root root  4096 Sep  7 08:47 .dbus

Notice that the format of the listing changed, and that new files are listed (specifically, filenames starting with a dot . are hidden from casual viewing).

We can also supply an argument, or target, for the command:

# ls -la /home

total 36

drwxr-xr-x.  6 root    root     4096 Sep 13 10:39 .

dr-xr-xr-x. 28 root    root     4096 Nov  7 14:58 ..

drwxrwxr-x.  5 grace   grace    4096 Nov  7 14:35 grace

drwx------.  4 harry   harry    4096 Sep 13 14:14 harry

drwx------.  2 root    root    16384 Sep  7 08:07 lost+found

drwx------. 24 student student  4096 Sep  7 08:56 student

Above, we instructed ls to retrieve a listing for the /home directory, even though we were not presently occupying that directory.  We also combined two options into a single set, rather than specifying each individually.  This is not always possible, but where it is, it simplifies command strings significantly.

As you progress in your studies, recall the basic structure of Linux commands.  So often, when commands are failing, it is because we have failed to implement the basic syntax correctly.

--help, man,  info – Finding out what to type

If you know a command but don't quite remember what goes after it, try tab completion.  You can also try putting --help after the command.  In many cases this will bring up a brief help page, giving you the needed clues. 

If you need more detail about a command you can use the built-in manual pages, accessed via man command-name.  Use the letter q to exit the man page reader.  To search within a man page, you can use /pattern (forward search), n (next pattern), N (previous pattern), and ?pattern (reverse search).  These shortcuts also work in less.

If you don't know what the name of the command you need is, you can try man -k pattern.  This will return a list of man pages which match pattern.  The man page system (and the -k search feature) depends on a small built-in database.  Under most circumstances it will be automatically updated as you install/remove software.  If it does not, you can update the manually database by running makewhatis.

Some commands will have a more advanced style of manual page which incorporates hyperlinks and colors.  These can be accessed using the info command.  If an info-style page is not available, info will display the standard man page.  Of particular use is info coreutils.  For more info, info info.

Module 1:
Getting around in EL6

yum update, install, epel, bash-completion

We will first update the system and install a handy little application called bash-completion using the yum command.  yum is the standard software package manager for EL6.

# yum -y update. 

The -y option tells yum to presume the answer to any question is "yes".  yum will go to a preconfigured software repository (or repo), download and install all required updates. 

We now need to install bash-completion.  The bash-completion feature is not distributed with EL6, but is with EL7.  It is one of the most useful tools when working with bash as it will autocomplete commands or suggest possible completions of a command.  To obtain it, we will need to configure yum to look for software in a different repository called Extra Packages for Enterprise Linux.  This is done through yum install epel-release.  This creates a file /etc/yum.repos.d/epel.repo which tells yum where to look to for software.  We can then install bash-completion:  # yum -y install bash-completion.  To get the benefits of bash-completion you will need to logout (exit) and log back in.

In RHEL6 proper, this is a little more involved; see Red Hat Specifics at the end of this module.

Typing at bash

There are lots of tricks you can do at the bash prompt; many are covered later, but there are a few you should know about now. 

You can use the up and down arrows to access previous commands.  You can edit the command by simply arrowing back to the appropriate place and typing.  You can jump to the beginning or end of a line by hitting CTL-a or CTL-e.  You can stop a running command by typing CTL-c.  You can also abort the current input line this way. 

You can also issue the command history which will display the history file with numbers prepended.  You can reissue that command by simply typing an exclamation point (called a bang !) followed by the number (no spaces).  Two bangs !! will reissue the last command.  A bang dollar !$ will reissue the arguments of the last command.

Below we ran a ping to test connectivity to a server, terminated the ping with CTL-c, then used ssh !$ to establish a terminal session to the remote server.

# ping 192.168.1.155

PING 192.168.1.155 (192.168.1.155) 56(84) bytes of data.

64 bytes from 192.168.1.155: icmp_seq=1 ttl=64 time=0.964 ms

64 bytes from 192.168.1.155: icmp_seq=2 ttl=64 time=0.205 ms

^C

--- 192.168.1.155 ping statistics ---

2 packets transmitted, 2 received, 0% packet loss, time 1733ms

rtt min/avg/max/mdev = 0.205/0.584/0.964/0.380 ms

# ssh !$

ssh 192.168.1.155

FIPS mode initialized

Capitalization matters:  File, file, FILE, and filE are four separate things as far as Linux is concerned.  As a general convention, most things are all lower case.

Often a command will produce more output than will fit on a single screen, or produces output which we want to use as input to another command, or which we want to save to a file.  To accommodate this we use redirection. 

The simplest redirection is the pipe – represented by the vertical bar |.  The pipe takes the output of one command and uses it as the input of the next.  For instance, listing the contents of the /etc/ directory using # ls /etc/ produces a lot of text.  The command less allows us to view text one page at a time.  By placing them on the same line, the output of ls is piped into less:   # ls /etc/ | less. 

Another common use of the pipe is 'piping through grep'.  grep is a command which can find lines containing a regular expression.  Much more is to be said about that later.  For now let's just look at the output of the ip a command, which will show our current IP addresses.  If we only wanted to see the lines containing inet (where the actual addresses are displayed), we could # ip a | grep inet.

If we wish to save the output of a command to a file we can redirect it using greater than >.  This will place the output into the file, creating it if it doesn't exist, and overwriting any other contents if it does.  For instance, if you wanted to save the output of the ip a command to a file, you would # ip a > file.  You could then view the contents of that file using less file or cat file, which will simply display it to the screen.

Note that bash opens all files and commands on a line at the beginning of command execution, thus cat file > file, opens and empties file before beginning to cat file.  The result is file will be emptied.

To add the output from ip route to my file use two greater thans >>, which will append to the end of the file:  # ip route >> file.  If you had only used a single greater, it would have overwritten the file.  If you used a single greater with no command before it, thus: # > file ; it would erase the contents of the file by overwriting it with the output of nothing.  This is often used to empty a file (such as a log), without changing its permissions or ownership.

You can string multiple redirections together to produce the desired results.  If you want a file containing the output of ip a and ip route, but only the lines containing 192 addresses in it you could: # ip a | grep 192 > file ; ip route | grep 192 >> file.  In this example the semicolon separates two commands, which are run as if they were on separate lines. 

Unix style systems have a several special virtual files:

*   /dev/null – A black hole, the bit bucket, a place where data goes and doesn't come back.  Unwanted output can be redirected here.
    It can also be used as a source of 'nothingness': cat /dev/null > file1 will replace the contents of file1 with nothing, making it empty.  > file1 is equivalent to this.
*   /dev/random – The source of high quality random data, generated from entropy gathered by the system hardware.  It can be temporarily emptied by reading it faster than entropy occurs.
*   /dev/urandom – A source of lower quality randomness.  It uses some system entropy, but augments it with a pseudo random number generator.  Not considered good enough for cryptographic purposes.
*   /dev/zero – an unending source of 0s.  Used to make an empty file.  Note that these are binary zeros, they will not display as text.

In bash there are three "standard streams".  These are data streams flowing into and out of a command.  Each has a designated number known as a 'file descriptor':

*   STDIN – 0.  The input to a command, either from the terminal, or a pipe.
*   STDOUT – 1.  The result of a command
*   STDERR – 2.  Any error messages from a command

Under most conditions STDOUT is either displayed on a terminal, or passed to a redirection.  STDERR is by default displayed on the terminal which invoked the command, not passed to a redirection.  The standard streams can be redirected using the appropriate descriptor:

*   command 2> errorfile – redirects STDERR of command to errorfile
*   command 2> /dev/null – sends STDERR of command to the void
*   command 2>&1 > file – redirects the STDERR of command to STDOUT, which will then be passed into the redirection to file.

    *   This can also be written as command > file 2>&1 or command &> file
*   command 0< file – use contents of file as STDIN to command

    *   often abbreviated command < file

You can also make the execution of a second command dependent on the success of the first: 
# cmd1 && cmd2 – will run cmd2 only if cmd1 is successful.
# cmd1 || cmd2 – will only run cmd2 if cmd1 exits with an error code. 

All processes (and a command is just a process) exit with a code.  By convention a code of 0 indicates success with no error, and all others indicate an error.  The last exit code is stored in a special variable $? which is displayed using # echo $?

A command can be run in the background by appending an ampersand: yum update &.

There are times you just want to get a good clean terminal to type at.  This can be done with CTL-l or by issuing the clear command.  It can also happen that you confuse your terminal by trying to print unprintable characters.  This usually is the result of trying to display a binary encoded file, or having a program crash while it's updating the screen.  To get everything straightened out, reset.

screen

We will install a small utility called screen, which allows switching between virtual screens (or windows). 
# yum -y install screen

Best practices say that the first command you issue in a terminal session should be screen.  We will make modifications so that will automatically happen later.  screen is required by STIG as it is one of the two common ways to lock a console (the other being vlock).  Neither will hide the terminal buffer, so someone viewing your console through putty or a similar product will be able to scroll back and see what you were doing.

When screen is run it opens a new window and enables the hot key sequence CTL-a, which alerts screen to an incoming command.  Common commands following CTL-a include:

*   x – lock the screen
*   H – log all activity to ~/screenlog.X.
*   c – create a new window
*   "  – list all windows
*   0-9 – jump to numbered window.
*   n / p – next / previous window
*   CTL-a – toggle between two windows
*   k – kill the current window
*   d – detach all windows, returning to the original bash session

Detached windows will remain active and logged in.  They can be reattached either from the same session, or a different one using screen -r.  Using the -R switch instead will reattach if a window is available, or create a new one if not.  Adding the -L switch starts screen in logging mode.

The screenlog can be displayed with several commands, but view (which is a special invocation of vi) seems to work best.  To quit view, use the following sequence ESC, :q, ENTER. 
Full usage of vi is addressed later.

RHEL6 specifics

This configuration presumes an installation of EL6 using CentOS, Oracle or Scientific Linux, not an official Red Hat Enterprise Linux installation.  The initial configuration of an RHEL6 installation is a bit more involved. 

The network may need to be enabled by changing these settings in
/etc/sysconfig/network-scripts/ifcfg-eth0: 

ONBOOT=yes, NM_CONTROLLED=no.

Then restarting networking:
service network restart

You will then need to register and attach to the Red Hat repositories using subscription-manager. 

To enable the epel repositories for tools such as bash-completion:
wget http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
rpm -ivh epel-release-6-8.noarch.rpm

For security compliance you should also disable Red Hat automatic updating by using chkconfig rhnsd off.  Alternatively you can enable download but not installation by setting retrieveOnly=1 in /etc/sysconfig/rhn/up2date.

Module 2:
Files and Directories

ls – listing files

To list the files in a directory, we would use the ls command.  When called without options or arguments, ls lists the contents of the user’s present working directory.  It will only display the names of files and subdirectories, and will not list hidden files (files whose name begins with a dot .) when called this way.  This is the listing of the directory /test.

#  ls /test

binary  directory  file  link  source

There isn’t much information available to us in this view.  Let’s add some options.

#  ls -la

total 56

drwxr-xr-x.  3 root root    90 Jun  2 08:32

dr-xr-xr-x. 24 root root  4096 May 19 14:11 .

-rwxr-xr-x.  1 root root 41504 Jun  2 08:25 binary

drwxr-xr-x.  2 root root     6 Jun  2 08:23 directory

-rw-r--r--.  1 root root    58 May 17 09:31 file

-rw-r--r--.  1 root root     0 Jun  2 08:32 hidden

lrwxrwxrwx.  1 root root    10 Jun  2 08:31 link -> /test/file

-rw-r--r--.  1 root root  2724 Jun  2 08:27 source

Here we’ve supplied two options to the ls command: -l and -a.  The -l option instructs the command to display a long listing of directory contents.  The -a option causes all files to be displayed (including hidden files such as .hidden in the output).  Together, these options provide the results we see above.

As we will be using the ls command very frequently, let’s take a moment to familiarize ourselves with the output.

drwxr-xr-x.  2 root root     6 Jun  2 08:23 directory

The underlined part is the permissions string.  The first character indicates the type of file we’re dealing with.  Here it is d, for directory.  We might also see an l (link), a dash - (regular file), or other characters intended to provide hints about the nature of a given listing.

The rest of the string shows permissions triplets for a file’s owner (user), the owning group (group), and anyone else (others).  In this string, r indicates Read, w is Write, and x is eXecute.  We could read the permissions string above as:

*   User: Read, Write, Execute
*   Group: Read and Execute (but not Write)
*   Others: Read and Execute (but not Write)

The dot . on the end of the permission string indicates that there is currently no Access Control List (ACL) associated with this file.  If an ACL had been associated with this file, we would see a plus sign +  rather than a dot.  We’ll discuss permissions (including ACLs) in detail in a later lesson.

drwxr-xr-x.  2 root root     6 Jun  2 08:23 directory

The 2 is the number of links to a file.  Links are entries in a directory that point to a file.  These come in two flavors: hard and symbolic.  Hard links point directly to the hardware location of a file (the inode) while symbolic links are like hyperlinks, and simply contain a path to another file.  The number increments as the number of hard links to a file increases and decrements as links are removed.  We will cover linking in depth during our discussion of file systems.

The next two fields indicate the owning user and group.  In this case, the owner is the root user, and the owning group is the root group.

The last three fields represent the size of the file (6 bytes), the date and time the file was last modified (June 2nd at 8:23 AM), and the name of the entry – directory.

file and stat

Let’s take another look at the output of ls -la:

#  ls -la

total 56

drwxr-xr-x.  3 root root    90 Jun  2 08:32

dr-xr-xr-x. 24 root root  4096 May 19 14:11 .

-rwxr-xr-x.  1 root root 41504 Jun  2 08:25 binary

drwxr-xr-x.  2 root root     6 Jun  2 08:23 directory

-rw-r--r--.  1 root root    58 May 17 09:31 file

-rw-r--r--.  1 root root     0 Jun  2 08:32 hidden

lrwxrwxrwx.  1 root root    10 Jun  2 08:31 link -> /test/file

-rw-r--r--.  1 root root  2724 Jun  2 08:27 source

In the above output, we have helpfully named each file to reflect its nature (file is a file, directory is a directory, and so on).  Outside of the classroom, this will rarely be the case.  Filenames frequently have no bearing over content.  For example, this is a partial listing of the /usr/lib/udev directory on the example server:

# ls

accelerometer     mtd_probe      tascam_fw

ata_id            mtp-probe      udev-add-printer

cdrom_id          rename_device  udev-configure-printer

The filenames are not especially revealing.  If we want to know more about these files, we should use the file command.

The file command will attempt to determine the nature of any file supplied to it as an argument.  It does this by running three sets of tests against the file, in this order: file system tests, magic tests, and language tests.

Briefly, file system tests examine the results of a stat call.  For example, executing ls in the /test directory of our example server shows a file called “link”. 

#  ls

binary  directory  file  link  source

Running file against link gives us some interesting results: 

#  file link

link: symbolic link to '/test/file'

#  stat link

File: ‘link’ -> ‘/test/file’

Size: 10             Blocks: 0         IO Block: 4096   symbolic link

Device: fd00h/64768d    Inode: 27204148    Links: 1

Access: (0777/lrwxrwxrwx)  Uid: (  0/  root)   Gid: (  0/  root)

Context: unconfined_u:object_r:default_t:s0

Access: 2017-06-05 10:45:27.808396471 -0500

Modify: 2017-06-02 08:31:57.946959353 -0500

Change: 2017-06-02 08:31:57.946959353 -0500

Birth: -

If we then call stat against link  it returns metadata associated with that file, including the denotation of symbolic link.  This demonstrates that the file system itself could understand what type of file link was, and the file command essentially queried it in the first wave of tests.  If this set of tests fails to get a satisfactory result, file will attempt identification through magic database files. 

For example:

#  file binary

binary: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.32, BuildID[sha1]=bb794ad0b7a9b70f6bb8d757d4423c2a374dabcf, stripped

#  stat binary

File: ‘binary’

Size: 41504           Blocks: 88         IO Block: 4096   regular file

Device: fd00h/64768d    Inode: 27204150    Links: 1

Access: (0755/-rwxr-xr-x)  Uid: (  0/  root)   Gid: (  0/  root)

Context: unconfined_u:object_r:default_t:s0

Access: 2017-06-05 14:01:15.692750865 -0500

Modify: 2017-06-02 08:25:27.684384663 -0500

Change: 2017-06-02 08:25:27.684384663 -0500

Birth: -

Above, file successfully identified binary as an ELF 64-bit LSB executable binary.  However, the results of stat indicate a type of regular file – the file system tests could not have correctly identified this file.  In this case, the magic files were consulted, specific byte patterns were matched in the file’s data blocks, and an identification was made.

If these tests both failed, the file command would attempt to determine if the target file was a text file containing character sequences from a known language.

which, whereis, locate

There are many ways to locate files in Linux.  The which command will attempt to locate the first instance of a named command in a user’s PATH.  The PATH environment variable  contains a series of directories, separated by colons :, through which the shell will search to find a command.  You can display the contents of PATH like this:

# echo $PATH

/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/root/bin

# which cat

/usr/bin/cat

Here, which searched sequentially for cat  in /usr/local/sbin, /usr/local/bin, and /usr/sbin before locating cat in /usr/bin.  If another copy of cat existed in the final directory (/root/bin), which would not have found it.  If other copies of the cat command existed on the system, in directories not referenced by a user’s PATH, which would be similarly unaware of them.

The which command tells us precisely which instance of a command will be executed when called without specifying a path to the command.  If that doesn’t seem important, consider this:

# echo $PATH

.:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/root/bin

Notice the dot at the front of the PATH.  That represents the present working directory.  If it is present in a user’s PATH, it can result in unintended execution.  For example, if a script called ls existed in a user’s present working directory, and the user then attempted to list the contents of that directory, he or she would inadvertently trigger the script instead.  The which command would be helpful in determining the source of the problem.

The whereis command is designed to locate binary, source, and man pages for designated commands.  It does this by searching:

*   a predefined, hard-coded list of directories
*   any directories in a user’s PATH
*   any directories defined by the MANPATH variable

Calling whereis -l without arguments will return a list of directories the command will search as well as the types of files it expects to find there. 

# whereis cp

cp: /usr/bin/cp
/usr/share/man/man1/cp.1.gz
/usr/share/man/man1p/cp.1p.gz

Here, whereis found the cp binary in /usr/bin and two man pages in /usr/share/man.  The whereis command is rather limited when compared to modern search utilities, but it can still provide quick answers when called upon.

find

The locate command is a simple tool for finding files by name on your system.  It uses an index database /var/lib/mlocate.db.  This is updated by updatedb, which the anacron scheduler runs daily by default.  If directories or files have been created, and an administrator wishes to index them immediately, updatedb (or locate -u) may be run as root to achieve this. 

Using locate is straightforward:

#  locate pathfile

/test/pathfile

Here we can see that locate has returned the absolute path of the located file.  There are some drawbacks to locate, however.  Foremost amongst these is that locate will always treat the supplied argument as a string pattern.  It will match this string in whole or in part, regardless of where in the path the pattern occurs.  For example:

#  locate cp | head

/boot/extlinux/cpuid.c32

/boot/extlinux/cpuidtest.c32

/boot/extlinux/ifcpu.c32

/boot/extlinux/ifcpu64.c32

/boot/grub2/i386-pc/acpi.mod

/boot/grub2/i386-pc/cpio.mod

/boot/grub2/i386-pc/cpio_be.mod

/boot/grub2/i386-pc/cpuid.mod

/boot/grub2/i386-pc/lsacpi.mod

/etc/dhcp

<truncated>

Note that locate matched the cp string without any regard for location within the indexed paths.  The above command, in fact, returned 1362 results on the example server. (wc -l counts lines)

#  locate cp | wc -l

1362

This behavior cannot be directly modified.  To find the cp command using locate, you would need to resort to silliness like this:

#  locate cp | grep /cp\$

/usr/bin/cp

The locate command certainly has its place, but for serious work the find command is the better option.  find is one of the most powerful search utilities available in Linux.  It can be used to find files based on an attributes such as filename, timestamp, ownership and permissions, and more.  In the interest of brevity, discussion of this command will be limited to:

*   A description of the basic structure and syntax of find
*   Common or useful invocations
*   Scenarios in which find can be especially helpful

Defining a search space

If we call find without any options or arguments, it does this:

#  find

.

./file

./directory

./directory/subfile

./binary

./source

./link

./.hidden

./pathfile

Here, find has behaved similarly to ls -Ra ; it has listed the contents of the present working directory (including hidden files), and recursively listed the contents of subdirectories as well.  Had we been at / when we called find in this fashion, it would have listed every file and directory on the entire system.

A directory, or series of directories, may be provided to find as a search space.  The depth of search in those areas can be refined with the maxdepth and mindepth options.  Consider the following output:

#  find /1 -type f

./1/fileInDir1

./1/2/fileInDir2

./1/2/3/fileInDir3

./1/2/3/4/fileInDir4

./1/2/3/4/5/fileInDir5

Here we have a stack of directories (1 through 5), with a single file in each.  We told find to start looking for regular files (-type f) in a directory called “1” (and all subdirectories beneath it).  Let’s use mindepth and maxdepth to narrow the scope.

#  find /1 -mindepth 2 -maxdepth 4 -type f

./1/2/fileInDir2

./1/2/3/fileInDir3

./1/2/3/4/fileInDir4

Here we can see that the search scope was successfully restricted to a depth between 2 and 4, as indicated by the highlighted output.

Searching by name

Suppose we need to find a configuration file, but we’re not sure of the name.  We know it ends with conf and it starts with a c, but we’re not sure of the capitalization.

# find /etc -iname "c*" -name "*.conf"

/etc/pki/ca-trust/ca-legacy.conf

/etc/abrt/plugins/CCpp.conf

/etc/security/chroot.conf

/etc/openldap/check_password.conf

Let’s break it down.

*   findstart finding
*   /etcstart here and recurse through all subdirectories
*   -inamesearch by name, ignore case
*   c*filename starts with “c”.  asterisk translates to “anything or nothing”
*   -namesearch by name, respect case
*   *.conffilename can be anything or nothing as long as it ends with “.conf”

The default behavior of find when multiple name or iname options are supplied is to insert a logical AND between them.  If you would prefer find to operate using a logical OR, simply pass it the -o option.

Searching by attribute

Frequently, we may need to find files with unsafe or undesirable ownership, permissions, or attributes.  We may, for example, wish to find all executable files which are world writeable (a common security concern).  Or, we might want to list any files with Special Purpose Access Modes (SUID, SGID, or Sticky bits) set.  Maybe we’d like to find files that are owned by a particular individual (or owned by no one at all), or files accessed or modified within a certain time window.  find can resolve all of these issues, and more.  Consider this example:

#  ls -l

total 56

drwxr-xr-x. 3 root root    33 Jun 12 15:40 1

-rwxr-xr-x. 1 root root 41504 Jun  2 08:25 binary

drwxr-xr-x. 2 root root    21 Jun 12 13:05 directory

-rw-rwxr--+ 1 root root    58 May 17 09:31 file

lrwxrwxrwx. 1 root root    10 Jun  2 08:31 link -> /test/file

-rw-r--r--. 1 root root    60 Jun  9 07:55 pathfile

-rwxrwxrwx. 1 root root  2724 Jun  2 08:27 source

#  find . -type f -perm /o=w -perm /o=x  \
-exec ls -l {} \;

-rwxrwxrwx. 1 root root 2724 Jun  2 08:27 /source

Here we’ve first listed the contents of the /test directory with ls -l.  This will serve as a reference proof against the results of the find command.  We then executed the find command, calling it this way:

find . -type f -perm /o=w -perm /o=x -exec ls -l {} \;

What did this accomplish?  Let’s break it down:

*   findstart finding
*   .start looking in $PWD and proceed recursively through all subdirectories
*   -type fsearch only for regular files
*   -permmatch files with the following permissions
*   /o=wmatch any of the bits listed – listed are “o=w”, or “write” for “others”
*   -permmatch files with following permissions (logical AND with previous -perm)
*   /o=xmatch any of the bits listed – listed are “o=x”, or “execute” for “others”
*   -exec ls -l {} \;run ls -l against the results of find

In English, that is "Find any regular files, in my current directory or beneath, which are writeable and executable by the world.  Then, run ls -l on them."

Let’s explore a few examples of finding files that present security concerns:

#  find / -nouser

Calling find like this would return a list of all unowned files on the system.  When files are unowned, this is usually the result of user account deletion.  Calling ls -l on an unowned file might result in something like this:

-rwxrwxrwx. 1 root root  2724 Jun  2 08:27 source

-rw-r--r--. 1 1002 1002231 Aug  2  2016 unowned

Note the highlighted portions of the output above.  For the file source, we can see an owner of root, and an owning group of root. However, the file unowned shows only numbers.  These numbers represent, respectively, a User ID and a Group ID.  We are seeing them now because there is no user or group matching these IDs in the /etc/passwd and /etc/group files.  Thus, we say the file is “unowned”.

We might also be interested in finding files with undesirable attributes such as SetUID or SetGID.  These attributes allow files to be executed with the permissions of the owning user or group rather than the invoking user.  This is especially problematic when such files are owned by root or other privileged accounts.  We can locate these types of files with find:

#  find / -type f -perm /u=s -exec ls -l {} \;

-rwsr-xr-x. 1 root root 32008 Nov  5  2016 /usr/bin/fusermount

-rwsr-xr-x. 1 root root 61328 Nov  5  2016 /usr/bin/ksu

-rws--x--x. 1 root root 23960 Nov  5  2016 /usr/bin/chfn

-rws--x--x. 1 root root 23872 Nov  5  2016 /usr/bin/chsh

-rwsr-xr-x. 1 root root 27832 Jun 10  2014 /usr/bin/passwd

The highlighted portion above instructs find to locate files with the SUID bit set.  The exec option returned a full listing of the located files, allowing us to verify the results and learn more about the files in question.

Finally, we may wish to find files that have been accessed or modified within a certain time range.  The find command offers options for locating files based on these characteristics:

*   atime – Access Time
*   ctime – Change Time (when the contents of the file have changed)
*   mtime – Modify Time (when the metadata, e.g. permissions changed)

These options are easily misunderstood, and as such, are often misapplied.  All three options use 24 hour blocks to define time ranges, and the timeline points backwards in time.  Specifying the number 1, for example, causes find to return files with a timestamp BETWEEN 24 and 48 hours old. 

If we had intended to locate files created within the last 24 hours, we would instead have used:

find / -atime -1

And, if we had wanted file more than TWO days (48 hours) old, we would have called:

find / -atime +1

cat, less, more, head, tail

Reading logs, config files, shell scripts, and other text files is a routine task for any Linux system admin.  In this section, we’ll discuss several of the most common and useful tools for viewing text from the command line.  We will briefly cover: cat, less, more, head, and tail.

The simplest commands for viewing text, cat, is most often invoked like this:

#  cat file

these are the contents of file

file contains multiple lines

^ that was a blank line

this is the end of file

Above, cat was invoked without options, and given a filename as an argument.  You can see that cat responded by dumping the contents of the file to STDOUT.  For small files, this is ideal.  For larger files, you will want to use a paging utility like less or more.

cat can place line numbers into the output if requested (-n, or -b to number non-blank lines only).  This is handy for debugging scripts or run files.

If you need to create a quick text file, but don’t want to fuss with an editor, cat can be called like this:

#  cat >> outfile

we are just typing in the empty space

this is a new line.

when we press CTL-d cat will close and append this to outfile

If the contents of a file are more than a single screen’s worth in size, you’ll want to consider using commands like less or more.  These utilities break content into pages, allowing users to read through them at their own pace.  They can be invoked directly from the command line: less file  or they can receive input from a pipe: ls -laR / | more.

When dealing with log files, it is often helpful to view only the first or last few lines of a file.  This is because logs are appended to sequentially, so the latest entries will be at the end of the file, and the earliest will be at the top.

If we wanted to know about only the last six lines logged by the ldap server, we might try this:

# tail -6 /var/log/ldap.log

Jun 12 09:19:39 server slapd[2447]: daemon: activity on 1 descriptor

Jun 12 09:19:39 server slapd[2447]: daemon: activity on:

Jun 12 09:19:39 server slapd[2447]:

Jun 12 09:19:39 server slapd[2447]: daemon: epoll: listen=7

Jun 12 09:19:39 server slapd[2447]: daemon: epoll: listen=8

Jun 12 09:19:39 server slapd[2447]: daemon: epoll: listen=9

The -6 option above tells the tail command how many lines to return.  If we instead supply the -f (follow) option, tail will display the last few lines of a file and continually refresh that output as the file changes.

Conversely, head returns the first few lines of a file.  Here’s the output of dmesg | head -5:

# dmesg | head -5

[    0.000000] Initializing cgroup subsys cpuset

[    0.000000] Initializing cgroup subsys cpu

[    0.000000] Initializing cgroup subsys cpuacct

[    0.000000] Linux version 3.10.0-514.el7.x86_64 (builder@kbuilder.dev.centos.org) (gcc version 4.8.5 20150623 (Red Hat 4.8.5-11) (GCC) ) #1 SMP Tue Nov 22 16:42:41 UTC 2016

[    0.000000] Command line: BOOT_IMAGE=/vmlinuz-3.10.0-514.el7.x86_64 root=/dev/mapper/cl-root ro crashkernel=auto rd.lvm.lv=cl/root rd.lvm.lv=cl/swap rhgb quiet LANG=en_US.UTF-8

The underlined portion is a wrapped line.  It shows the options supplied to the kernel at boot time. 

touch, tee, echo

Much of system administration in Linux involves editing text files.  Occasionally, we will need to create a new file in a command line environment.  For most work, we will turn to a fully featured editor such as vi, which is addressed later.

In other situations, we may only require that a file exist.  The file /.autorelabel, for example, will cause all files and directories on a system to be relabeled to their default security context if it exists at boot time. The file itself is empty, and does not exist by default.  The simplest way to create such a file would be to use the touch  command.

The intended use of touch is updating the access and modify timestamps on a given file.  However, if a non-existent filename is supplied to touch as an argument, touch will create it.  Here’s a brief look at touch in action:

# ls

# touch somefile

# ls

somefile

We might also wish to create a file to hold the output of a command or script.  In these cases, we would typically use command line redirectors like > or >>.  This will redirect all output which would have gone to STDOUT, which may not be desired.  To send output to both STDOUT and a specified file, we would use tee. To create small configuration files, or add lines to simple configuration files, we could use cat or echo with redirection.

The tee command is often used in scripting to send output to both STDOUT and to a designated file.  It can be called from a script (for simple logging) or directly from the command line when we want to both view the output of a command and save a copy of it for later perusal.

Here’s a simple demonstration of tee’s capabilities:

#  ls /usr | column | tee /cap

bin     games   lib     libexec sbin    src

etc     include lib64   local   share   tmp

#  cat cap

bin     games   lib     libexec sbin    src

etc     include lib64   local   share   tmp

The primary function of echo is to read input (typically from STDIN) and send that output to STDOUT.

We can exploit this behavior with command line redirection to insert text into files.  This is useful for appending lines to configuration files, or creating small text files (e.g. /etc/exports for quick NFS sharing).

#  echo "this is line 1" > file

#  cat file

this is line 1

#  echo "this is line 2" >> file

#  cat file

this is line 1

this is line 2

mkdir, rm, rmdir, cp, mv

Directories can be created with the mkdir command.  The use of this command is relatively straightforward; simply invoke mkdir and provide (as an argument) the path and name of the directory you wish to create.  Let’s try it out:

#  mkdir -m 0777 -p this/is/insecure

#  find this -exec ls -ld {} \;

drwxr-xr-x. 3 root root 16 Jun 16 15:26 this

drwxr-xr-x. 3 root root 22 Jun 16 15:26 this/is

drwxrwxrwx. 2 root root 6 Jun 16 15:26 this/is/insecure

The rm command removes (deletes) files and directories.  This is an inherently dangerous act; thankfully, rm has options to limit its scope and effect.

*   rm – remove a file
*   rm -r – remove a directory (and everything inside it)
*   rm -i – prompt user for confirmation before deleting
*   rm -f – force - for when you absolutely, positively must destroy

In EL6, the .bashrc file for the root user will contain a default alias of rm to rm -i. This causes rm to prompt the user for confirmation before deleting any file.  From a safety and security standpoint this is a desirable behavior, but it presents a problem when root needs to remove a large number of files. In these cases, we may use rm -f or invoke the system version of rm directly (instead of the bash built-in):

#  rm cap

rm: remove regular file ‘cap’? #confirmation prompt

#  /usr/bin/rm cap

#  #no confirmation

There is also a separate, related command for dealing with directories: rmdir.

To copy and move files, use cp and mv.  The functions of each should be obvious, but there are some factors to consider regarding their usage:

*   Copying a file requires read permissions on the original file, and read/execute on the directory containing it.  When the new file is created, it will be owned by the copying user and access permissions will not be preserved from the original.  The selinux security context for the new file will be inherited from the directory it is created in.
*   Moving a file does not require any permissions on the file itself; instead, the user would require read, write, and execute privileges on the directory containing the original file.  This is because file deletion is a directory operation.  Rather than saying a file was deleted or moved, we should say that the directory listings for this file’s inode were altered.  It is therefore unsurprising that moved files retain their security context, ownership, and permissions.

sort, wc, tr, uniq, diff

Linux command output is sometimes difficult to parse and understand.  The specific information we are searching for may be lost in a wall of irrelevant or oddly formatted text.

The sort command can arrange such information alphabetically, by numerical order, or by other characteristics (such as days of the month).

#  cat list

red

blue

green

#  cat list | sort

blue

green

red

We can use the wc command to get counts of words, characters, or lines in a file or input stream:

# cat counts

This file contains five lines.

The number of words is 29.

I don't know the number of characters.

But I can use wc to find out.

Let's try it.

# wc counts

5  29 141 counts

# wc -c counts

141 counts

# wc -l counts

5 counts

# wc -w counts

29 counts

The tr command allows us to translate specified characters into other characters (or remove them altogether).  Here are some simple examples using command line redirection.

Translating lower to uppercase:

# ps

PID TTY          TIME CMD

3271 pts/0    00:00:00 bash

3418 pts/0    00:00:00 ps

# ps | tr [:lower:] [:upper:]

PID TTY          TIME CMD

3271 PTS/0    00:00:00 BASH

3419 PTS/0    00:00:00 PS

3420 PTS/0    00:00:00 TR

Squeezing out the repeating spaces to make things more compact:

# ps | tr -s [:space:]

PID TTY TIME CMD

3271 pts/0 00:00:00 bash

3428 pts/0 00:00:00 ps

3429 pts/0 00:00:00 tr

Deleting numbers from the output:

# ps | tr -d [:digit:]

PID TTY          TIME CMD

pts/    :: bash

pts/    :: ps

pts/    :: tr

Deleting everything that ISN’T a number:

# ps | tr -cd [:digit:]

327100000003437000000034380000000

Finally, remember that tr is translating characters rather than words:

# ps | tr 'bash' 'shell'

PID TTY          TIME CMD

3271 pte/0    00:00:00 shel

3463 pte/0    00:00:00 pe

3464 pte/0    00:00:00 tr

Note that tr didn’t replace “bash” with “shell”.  Instead, it replaced “b” with “s”, “a” with “h” and so on.  This is why “pts” became “pte”.

The uniq command can be used to find lines that repeat (or lines that don’t), but it has some limitations.  For example, uniq can only find lines that repeat immediately.  If a duplicate line exists in multiple locations in a file, and each duplicate line is separated by some other unique text, uniq will not register this as a duplicate.  Consider the following example:

# cat song

This is the song that never ends

it never ends

it never ends

It just keeps going

it never ends

it never ends

# uniq song

This is the song that never ends

it never ends

It just keeps going

it never ends

The diff command is used to compare two files.  This is typically used as a form of version control for configuration files or for forensic purposes.  Consider the following example:

# diff file1 file1.bk

1,4c1,4

< This is the original file

< and nothing has been changed

< but we'll make some changes

< and compare it with diff

---

> This is the copied file

> and something has been changed

> we made some changes

> and compared it with diff

5a6

> we added this line

We can read the output this way:

1,4 lines 1 through 4 of the first file
cneed to be changed
1,4to match lines 1 through 4 of the second file
5a6and we need to add line 6 of the second file after line 5 in the first file.

We can see that only four lines were returned from the first file.  Why did diff insist that a changed needed to be made after line 5?  Let’s compare the files side by side with line numbers:

# diff -y file1 file1.bk | tr -s [:space:] | cat -n

1  This is the original file     |   This is the copied file

2  and nothing has been changed  |   and something has been changed

3  but we'll make some changes   |   we made some changes

4  and compare it with diff      |   and compared it with diff

5  but this line won't change        but this line won't change

6           > we added this line

Note lines 5 and 6 above.  Both files contain an unaltered line 5, which diff did not display.  Line 6 existed only in the second file.

Module 3:
vi

There are several text editors that come with EL6.  There is gedit – a graphical, notepad-like editor, nano – a text based editor developed originally as part of an email client, and then there's vi.  Unlike gedit or nano, vi is not intuitive.  It has a steep learning curve, such that even the people who love it will admit that it takes weeks or months to truly get comfortable with it. 

To begin with, it uses modes: Insert mode allows you to type; Visual mode allows you to select; and so-called Normal mode allows you to run commands, open and close files, etc.  Every beginner finds themselves flopping around in the wrong mode, trying to type in normal mode and watching weird things happen instead.

So if it's not intuitive, takes a long time to learn, and has easier alternatives, why bother? 

*   If you do spend some time getting good with vi, you will find it is the right tool for many jobs.  With the extensions provided in vim (vi improved), it is a pretty fully featured programming environment, with lots of handy shortcuts and support for most of the major languages.  It is the preferred development environment for many programmers, to the point that people even pay for versions of it to run in Windows.
*   In a Unix-like environment, it is the only editor you are sure to have.  Graphical editors, like gedit, don't run without graphics, and real servers don't run graphical interfaces.  Other editors, like nano, will not be available.  vi is available and installed by default on pretty much every device where you can run ls to get a directory listing.  As long as the computer in front of you isn't running Windows, it probably has vi.
*   Some tasks, such as editing the password file directly can only be accomplished using vi.

In EL6 installations, there are two versions of vi installed:  vim-minimal  and vim-enhanced, which has all the pretty colors and extra features.  Users with a UID less than 200 will get vim-minimal by typing vi, those above (all regular users) will get vim-enhanced.  This is due to aliases set in /etc/profile.d/vim.*.  All users will get the enhanced version by invoking vim.  If a file should not be changed, you can also use view, which is vi with write disabled.

This module is broken into three parts: the first is the absolute least you need to know to be an effective administrator; the second is a list of some of the cool things that may make your life easier if you learn to use them, the third addresses safe editing of configuration files.

The Basics

At a minimum you need to be able to open a file, edit it, and get out without breaking things.  To open a file, vi newfile.  You will be in Normal mode. To begin typing you will need to be in Insert mode; to get there you can use

*   i – insert here,
*   o – add a line below and insert, or
*   A – insert at end of current line.

You can use the arrow keys to move in any mode.  To get back to Normal mode press esc. 

Getting around in Normal mode:

*   u – undo
*   ctrl-r – redo
*   yy – 'yanks' (copies) the current line,
*   dd – cut current line,
*   p – paste
*   ^ / $ – beginning/end of line
*   H / M / L – high/mid/low on page
*   gg / G – top/bottom of file
*   * / # – match next/previous word under cursor

    *   Repeating commands:

        *   .  – (dot) repeat the last thing you did
        *   or a number before the command:  10dd cuts 10 lines, 2p pastes twice.

To select, you need to be in Visual mode.  From Normal press

*   v – selects characters
*   V – selects lines
*   CTL-v – selects blocks
*   y – copy
*   d – delete
*   p – paste

To exit vi, go to Normal mode then issue a vi command. Commands begin with a colon:

*   :q – quit without saving, if you made changes it will want :q!
*   :e! – start editing the file over without saving
*   :w! – write changes to file

    *   :w! /path/otherfile – writes to otherfile
    *   :w >> otherfile – appends buffer to otherfile
*   :wq! – write and quit, the most common way to leave

Cool tricks and Pretty colors

Most of the things in this module apply both to vi (vim-minimal) and vim (vi-enhanced).  Some, such as the syntax aware highlighting (the pretty colors) only apply to vim.

Multiple files

You can open several files sequentially: #vi fileone filetwo filethree.  Each will open in a separate buffer.  To move between buffers :n – next or :N – previous.  If you haven't written your edits out, use :wn (write, next) or :n! (next, discard changes).  To list buffers  :ls.  To leave all files at once :wqa!.

You can also open a second file in the current buffer  #vi filethree, then :e filefour.  To switch between them, use CTL-^. 

We recommend using either of these methods, but not both, as it can get confusing.  If you do get confused while doing these kinds of things CTL-g will give you a hint as to where you are and what you are doing.

If you want to open multiple files on a single screen, open one normally then :split otherfile.  To move between windows CTL-w followed by an arrow key.  With no arguments, :split will open the current file in two windows – very useful if you want to view the original while making changes.  To view side by side :vsplit (vim only). 

Another interesting thing is that vi will open remote files using scp, http, or ftp:
#vim scp://user@other.server.com//var/log/messages. 

Inserting stuff

There are lots of ways to get external content into a file.  The most basic is to open multiple files, select what you want, switch files and paste.  For instance to put the entire contents of file2 into file1:  #vi file1 file2,  :n,  gg,  V,  G,  y,  :N,  p.  That's a lot of keystrokes for a pretty small result.  Instead we can issue commands thus  #vi file1,   :r file2.  This reads the contents of file2 into file1 at the cursor.

To insert the result of a command into a file  :r !date      
…or even     :r !ls -la | grep pattern.

There are times you may wish to carry lots of different cut text at the same time.  To cut and paste to multiple registers (clipboards) you need to specify a register name.  This is done in Normal mode.  Registers are specified by double quotes and a letter.  For instance to copy a line into register x and paste it three times  "xdd,   "x3p.  You can see the contents of all registers with :reg. 

Avoiding repetition

If you find yourself typing the same thing over and over again you can create an abbreviation for it.  For instance, here is a typical address record from a DNS zone file:
server1INA10.0.1.5
These files can go on for hundreds of lines and mistakes can cause service outages.  To avoid some of the drudgery and chance of error:

:abbr ad    IN    A    10.0.1.

Now you can simply type server1 ad  followed by a space and ad will expand to fill
the   IN   A    10.0.1. in the middle.

You can add abbreviations to a vimrc/virc file and they will be there every time you run vi.  To find the path to the appropriate file :version.

There are some global commands which you can use.  They take the general form of
:g/pattern/command   These can go well beyond the scope of this course but some handy ones to know about include:

*   :g/apple – show lines containing apple
*   :g/apple\|orange/d – delete lines with apple or orange
*   :v/apple\|orange/d – delete lines without apple or orange
*   :%s/apple/orange/g – search for apple, replace with orange, globally
*   :g/^\s*$/d – delete lines that are whitespace \s* from beginning ^ to end $.  That is to say, blank lines.

If you want to repeat a vi command, use the up arrow after a colon.  If you find yourself doing the exact same set of keystrokes repeatedly you can record a macro to a register from Normal:

*   qM – begin recording to register M

    *   perform your action
*   esc, q – end recording
*   @M – perform action saved in register M
*   @@ – repeat

Running commands

You can run commands external to vi from Normal mode, e.g.   :!ip a   or  :!bash

If you want to run an external command on the contents of your file   :% !sort, where the percent sign represents the contents of the file.  To run commands by line number it is best to first see the line numbers   :set number   (:set number! turns them off).  Now you can say something like :4,12 !sort -u, which would sort lines 4 through 12 keeping only the unique lines. 

You can also run commands on a selection using Visual mode.  Simply select what you want – (V is best for line based operations) then run the command using !cmd. Do not esc to Normal; do not add a colon, vi will do it for you.  It will put in this :'<,'>! cmd where the tick and bracket collection means the beginning and ending of the selection.

Moving around quickly

If you find yourself moving back and forth in a large file, you can create marks with letters assigned to them.  From Normal, press m followed by a letter.  To return to that mark, use the single quote  '  followed by the letter.  To list current marks :marks.  Marks made with a capital letter will carry from file to file (within a session).  To perform an action between two marks :'x,'y !sort -r.  To move to the last position before a jump ''.

Other quick movement methods include:

*   w / b – move a word forward/backward
*   f char – find char, F searches backwards
*   % – find the matching delimiter )]} – useful when programming
*   /pattern  –  search for pattern, n for next, N previous, ? search backwards

Other things

To find help  :help.  (vim only, help will be completely munged in vi)

To see matching topics :help pattern, followed by CTL-D or tab.

In Normal, place the cursor over a word, K will take you to the man page for that word.

To enable/disable the pretty colors  :syntax on/off

If you have a crash or lose connection during a session :recover filename.

If you get discouraged  :help!

Editing Config Files

Most configuration of EL6 is done by editing plain text files.  In most cases even menu-based Text User Interfaces (TUIs), Graphical Tools, and command line utilities are ultimately just making changes to configuration files that you can also edit manually.  Most of these files are located in the /etc directory or sub-directories below it.  There are different types of config files with differing conventions but there are generalizations that can be made:

*   Anything starting with a hash # is a comment and will be ignored by the system.
*   White space, either vertical or horizontal does not matter.  It is there for humans, not computers.
*   Order of options in a simple list will not matter either.
*   To turn an option on, set it to 1; 0 will turn it off.
*   Changes made to a config file will not be effective until the service calling it is restarted.

    *   In EL6 this is done with the command service service-name restart.

There are exceptions to all of these rules, so read the documentation before making changes.

There are several ways to protect yourself when editing a config file.  The simplest is to make a habit of either making a backup copy using the cp command, or writing the vi buffer to a different filename before you begin typing using :w! file.conf.backup. 

Another standard way is to not change the base file.  Many services will have a standard configuration file (such as /etc/crontab for the cron service) and a separate directory for user generated changes (/etc/cron.d/).  Some services will even place user-specific files either in a user's home directory or another user-specific directory.  For instance, user configuration of cron will be in /var/spool/cron/username/.  Thus the basic, unchanged configuration can be restored by simply deleting or moving the changed files.

Sometimes a change being made has the potential to break access to a computer, or may make the machine otherwise unusable.  Changing the IP address of a machine is one such change.  The way around this problem is to backup the file to be changed, then schedule a task in the future that will the restore original unless the task is canceled.  If you are locked out, the task will run and everything will be as it was before the change.  If your change was successful, you merely need to log in and delete the task before it runs. 

Module 4:
Users and Groups

useradd – Adding users

So far we have been logged in as the superuser root.  This is bad practice.  Instead each user should be logging in as a unique individual.  To do this we will need a user account for each user.  When a user is created with the command useradd, by default several things happen: 

1.  The files /etc/default/useradd and /etc/login.defs are consulted
2.  A primary group is created for that user by adding a line to /etc/group.
3.  A line is created in /etc/passwd assigning them a User ID (UID), a primary group, a home directory, and a login shell. 
4.  A line is created in /etc/shadow (where the password hashes are stored) – with no password hash. 
5.  A home directory is created in /home
6.  The contents of /etc/skel is copied the home directory.  This typically includes any user specific startup or configuration scripts such as bash_profile and bashrc. 
7.  A mail spool file is created for the user in /var/spool/mail.

/etc/default/useradd & /etc/login.defs

The file /etc/default/useradd, has seven fields:

*   GROUP – by default this is ignored.  But if useradd is invoked with -N (do not create a group for that user), it will be honored and the users default group will be 100 – users.
*   HOME – the path for home directories.
*   INACTIVE – this controls inactivation of accounts with expired passwords.  -1 will not disable accounts. 0 will disable the account immediately.  Any positive number will be the number of days between expiration and inactivation.  On a government system this should be set to 0.
*   EXPIRE – date that the user's password expires.  This is set either in days since the epoch (1 Jan 1970), or YYYY-MM-DD format.  In most cases this is left blank.  Do not set this to 0 while INACTIVE is also 0 as users created this way will never be able to log in.
*   SHELL – the default shell. 

    *   If you wish to create a non-interactive user (for instance for a service), use
        useradd -s /sbin/nologin instead.
*   SKEL – the default skeleton directory.  Anything in this directory will be copied to the home directory of all new users. 
*   CREATE_MAIL_SPOOL – a simple yes/no suffices.

There are several fields that must be set in /etc/login.defs on government systems:

*   PASS_MAX_DAYS – the maximum password age.  This should be set to 60.
*   PASS_MIN_DAYS – minimum time between password changes, Set this to 1.
*   PASS_MIN_LEN – the minimum password length.  This should be 15.
*   PASS_WARN_AGE – the number of days before password expiration occurs.  The default is 7; this may be short for some users.
*   FAIL_DELAY – the time in seconds between login attempts.  This is not a default field; it must be added and set to 4.

There are three other fields mentioned in the STIG:  UMASK 077, ENCRYPT_METHOD SHA512, and CREATE_HOME yes.  These are defaults and should not be changed.

/etc/group, /etc/passwd, /etc/shadow

When you add a user, a line like this will be created in /etc/group:  bob:x:508:
This simply says that there is a group called bob with a Group ID (GID) of 508.  If there were additional members of the group, they would be listed after the final colon.  The GID is simply the next one available.  This group is assigned to bob as his primary group in /etc/password. 

A line is created in /etc/password:  bob:x:506:508::/home/bob:/bin/bash 
This says (in order of the fields): there's a user bob, he uses a hashed password (x), his User ID is 506, his primary Group ID is 508, (an empty field), bob's home directory is /home/bob, and his shell is /bin/bash.  The empty field is called a GECOS field; it's named after a defunct protocol, and is now only used for comments or such things as "User Display Name".

A user's identity is established uniquely in a UNIX system by User ID.  By default useradd starts at the first available number, beginning with 500.  The numbers below 500 are reserved for system use.  This number, along with the Group ID is used for permissions and ownership.  If a user is deleted, the next new user will by default be assigned the old UID.  This could result in a new user 'inheriting' the files and permissions of the previous user.  Group IDs work the same way.  There are several ways to prevent this:

*   Manually specify a unique UID and GID.  The maximum UID defaults to 60,000.  This limit can be raised as high as 4,294,967,295 by editing /etc/login.defs. 
*   Never delete a user, lock their account instead.
*   Run a user deletion script that will find and remove the users files and folders before deleting them.

A line will be created in /etc/shadow:  bob:!!:17312:0:99999:7:::
This is where the actual security information lives.  This file is owned by root and should have no permissions whatsoever on it.  This says that bob exists and his password hash is !!  This is not a valid password hash.  The process that produces a password hash cannot produce the characters ! or *.  Therefore any hash with those characters in it will break the user's login.  This will change when bob's password is set.

The third field is the last time bob's password was changed in days since the epoch (1 January 1970).  If this field is set to 0 the user must change their password on next login.  The remainder of the fields are related to password expiration and such.

Almost all the default actions of useradd can be overridden by use of command line switches.  Commonly used switches include:

*   -G – add user to additional groups (no space, comma separated).
*   -p – password.  This is an encrypted value, not a simple plaintext password.
*   -s – use a different shell.  Often /sbin/nologin to prevent interactive login by that user.
*   -e – expire date in YYYY-MM-DD format
*   -u / -g– manually set the user or group ID

passwd, chage, usermod, userdel, newusers, chpasswd, vipw, vigp

After you have created a user you will need to set their password using passwd.  Common switches for passwd include:

*   -l / -u – lock and unlock a user's account
*   -e   – expire.  Forces a password change at next login
*   -x   – set maximum days for expiration
*   -S   – show status of the user's password

Password expiration for a user can be set with chage.  It can be viewed with chage -l.  Global password parameters are specified in /etc/login.defs as discussed above.

In EL6 a separate Pluggable Authentication Module (or PAM) can be installed to enforce password quality.  The STIG should be followed

Password quality rules are enforced by PAM – Pluggable Authentication Modules.  There are many files used to configure PAM and any changes to them should be approached with care, as you can permanently disable a system with a typo.  Account lockout, password encryption, and password reuse policies are configured in /etc/pam.d/system-auth and /etc/pam.d/password-auth – the guidelines in the STIG should be followed exactly as written. 

User account information can be modified by the usermod command.  Users can be deleted with userdel (-r removes their home directory and mail spool as well).  If you wish to create multiple users from a file, this can be done with newusers.  Passwords can be set en masse by using the chpasswd command.

You can also create and modify users and groups by editing the relevant files directly, though this is not recommended as it is possible to break a system pretty completely by making a mistake.  If it is at all possible, use the tools mentioned above. 

If the normal tools simply will not do the job, there are special editors provided which provide file locking and some level of sanity checking; these are vipw and vigp for the password and group files respectively.  With the -s switch, they can be used to edit the relevant shadow files.  There is also a visudo to edit the sudoers file which we will mention later. 

groupadd, groupmod, groupdel, groupmems – Building groups

As with users, groups can be manipulated with the corresponding commands: groupadd, groupmod, and groupdel.  Users can either be added to secondary groups on user creation (using the -G option), using usermod -aG or groupmems -g groupname -a username.

groupmems -l -g groupname can be used to list the members of a group. It will not however list the primary group member.

su, wheel – Becoming other users

As we said before, best practice is to never login as root.  A secure system will have strong controls on local root login and will not allow remote login as root at all.  This is configured by setting PermitRootLogin no in /etc/ssh/sshd_config.  To perform administrative work on such a machine, you must first login as a normal user (UID =>500). 

Once logged in there are a few options to elevate your privileges.  On a default installation, if you have the root password you can change to root by using the su (substitute user) command and entering the root password.  If you wish to execute commands in the environment (home directory, startup scripts, etc.) that root would have if logged in directly use su -   By default any user can su to any other user if they know the appropriate password.   Root can su to any other user with no additional authentication required.  Changing identity can sometimes get confusing.  If you are ever uncertain: whoami.  For more detail, id.

At the very least you will want to restrict the ability to su to root to a small group of administrators.  The special group wheel (GID 10) is designated as an administrative group.  To restrict use of su to only members of wheel.  First add the users with usermod -aG. Then uncomment the following line in /etc/pam.d/su:
auth required  pam_wheel.so use_uid. 

sudo, sudoers, chsh

Restricting su somewhat strengthens the security posture of a computer, but presents a problem as everyone who has a need for administrative control must have the root password.  It is also important to note that a user who has become root via su is root and will be audited as such.  It may be desirable to further restrict access.  This is done via use of the sudo command. 

When a user runs sudo the following command is executed as if it were run by root, but the user does not become root.  The user is prompted for their password, not for the root password.  After entering their password, that authentication remains valid a default of five minutes.  This timeout can be changed by adding Defaults    timestamp_timeout=X, where X is the timeout in minutes and -1 means "never timeout" to the file /etc/sudoers.  Remember, this file should only be edited with visudo, not with standard vi or vim.

Even during the authentication time period, an sudo user will still be required to type sudo before every root level command issued.  In bash the last command can be reissued by simply typing !!  If you type a command that requires sudo and get the dreaded Permission denied response, you can save time by reissuing it via sudo !!

By default the group wheel can run sudo and can execute any command as root.  After adding users to the group wheel or to /etc/sudoers, and verifying that sudo works correctly; you can prevent the use of the root account with the chsh (change shell) command:
sudo chsh -s /sbin/nologin root. 

To further prevent direct login by root all entries in /etc/securetty should be removed, leaving an empty file.  If you wish to allow root login from the local terminal only remove all entries except tty1.

Individual users or groups can be allowed a limited command set with or without a password.  For instance, the following line can be added to /etc/sudoers to allow a user in the group backup to mount and unmount cd/dvd media when logged in locally.
%backup  localhost=/sbin/mount /mnt/cdrom, /sbin/umount /mnt/cdrom

The amount of detail and granularity available in sudoers is beyond the scope of this course, but should be explored, based on local needs.

who, w, lastlog, last, lastb -- Who's where & when

As an admin, you often need to know information such as who is logged in, when they logged in, and what they are doing.  The who command shows who is logged in, when they logged in and from where; w shows all that plus some usage stats and the current command being run by that user.  These two commands rely on the database /var/run/utmp.  This database is also used by the command uptime.  The utmp database feeds login/logout information into several other historical databases.  The contents of these can be viewed with:

*   lastlog – /var/log/lastlog – last login of each user, sorted by UID. 
    Useful with | grep -v Never.
*   last – /var/log/wtmp – successful logins by time.  There is a pseudo-user called reboot who logs in on every startup.  To see all reboots: last reboot. 
*   lastb – /var/log/btmp – unsuccessful logins.

Module 5:
Ownership, Permissions & Access

Earlier in this course, we observed output similar to this:

# ls -l

total 56

-rwxrwxrwx.  1 root root    58 May 17 09:31 file

Where -rwxrwxrwx is the permissions string, and root root lists the owner of the file and the owning group. The first character of the permission string is not part of the permissions set, and is instead used to identify the type of file we are dealing with.  Starting with the second character, we see this: rwxrwxrwx. 

This string can be broken into 3 sets, denoting permissions this way:

Owning User:rwx (read, write, and execute)
Owning Group: rwx
Others:rwx

Or stated another way: U:rwx G:rwx O:rwx

The output of ls –l displays the permission string using alphabetic characters; the system sees them as 12 binary bits where Read = 4, Write=2, and Execute=1\. Each rwx triplet will evaluate to some decimal value between 0 and 7, for a total of 8 possible values.  Because of this, these permission strings are sometimes called “octal permissions”. The triplets can be treated as 4 concatenated 3 bit strings:

| String | Decimal | Binary | Meaning |
| --- | 0 | 000 | no permission |
| --x | 1 | 001 | execute only |
| -w- | 2 | 010 | write only |
| r-- | 4 | 100 | read only |
| -wx | 3 | 011 | write, execute – no read |
| r-x | 5 | 101 | read, execute – no write |
| rw- | 6 | 110 | read, write – no execute |
| rwx | 7 | 111 | read, write, and execute |

Changing Permissions

The owner of a file (or the superuser) can change the permission set on a file by invoking the chmod command.  The chmod command works with either octal: # chmod 755 list, or symbolic notation: # chmod u=rwx,g=rx,o=rx list.  chmod accepts the following symbols:

*   u – set permissions for the owning user
*   g – set permissions for the owning group
*   o – set permissions for all others
*   a – apply a permission to all: user, group, and other
*   = – set an exact permission
*   + – add a permission to an existing set
*   - – subtract a permission from an existing set

Special Purpose Access Modes

Earlier, we mentioned “12 bits” for permissions, but we’ve only discussed 9 bits (3 each for User, Group, and Others, respectively).  Now we will discuss the other three.

There’s a set of file behaviors referred to as Special Purpose Access Modes or SPAMs.  This set is comprised of: SUID, SGID, and something called the “sticky bit”.

SUID allows a file to be executed with the permissions of the file’s owner rather than the user who invoked it.  Normally, a script executed by a user could not perform any tasks that the user himself did not have permissions to perform.  With SUID, a script will be able to do anything its owner could do, regardless of who runs it.  This is obviously dangerous, and must be carefully implemented and monitored.

SGID is similar in concept to SUID, but it applies to the named group as opposed to individual user accounts.  SGID is best used on directories, where its effect will be to cause all new files created in that directory to be owned by the directory’s owning group (rather than the primary group of the creating user).

The “sticky bit” prevents anyone other than a file’s owner (or root) from deleting or renaming it, regardless of permissions.  Normally, any user with write and execute permissions for the directory a file inhabits can delete or rename the file.  The sticky bit prevents this.  Often, this is set on the /tmp directory (which, by nature, must be writeable and executable by many users).  Doing so prevents users from destroying temporary files they do not own.

The converted binary values for the three SPAMs are: SUID-4, SGID-2, Sticky-1.

The chmod command may be used to set (or unset) Special Purpose Access Mode values on files and directories:

# chmod 7777 list

# ls -l list

-rwsrwsrwt. 1 root root 15 Jun 19 09:49 list

Note the underlined characters.  The first 7 in the command chmod 7777 list causes SUID, SGID, and Sticky to be set on this file.  This is represented by the highlighted characters in the permission string ( rw[suid] rw[sgid] rw[sticky] ).  We can do this in symbolic notation as well:

# chmod u+s,g+s,o+t list

# ls -l list

-rwsr-sr-T. 1 root root 15 Jun 19 09:49 list

Note the uppercase T at the end of the string.  This indicates that the sticky bit has been enabled, but that others do not currently have execute permission on the file.  We would see similar behavior with SUID and SGID.

umask

To control permissions on new files and directories, we may use umask.  A umask consists of a set of permissions to be subtracted from the system default of 0777 when new files and directories are created.  Additionally a final check will remove  execute permissions from files when they are created.

For example, if the umask was 0027 the following would occur:

*   A new file/directory is created with default permissions of 0777
*   umask is subtracted from 0777, leaving 0750
*   If the target is a file, remove any execute permissions, leaving 0650

Issued with no arguments the command umask will return the current effective mask.  To temporarily set the mask, follow umask with the desired value:  # umask 0027. 

In EL6 the default umask for both system and regular users is 0077.  This is defined in /etc/bashrc, and can be changed there.  To set an individual user's default mask, place the desired umask command string into bashrc in their home directory. 

Note that the current umask has no effect on existing files.  It only affects permissions on new files created after it has been set.

File Ownership

There are two entities granted specific permissions to any file or directory: the owning user and the owning group.  Users may always change permissions (and ownership) on the files they own, even if they have no access to the files in any other sense.  Proper file ownership, therefore, is an important security concept.

To change ownership on a file, we would use the chown command:

# chown bob:sales list

# ls -l list

-rwxr-xr-T. 1 bob sales 15 Jun 19 09:49 list

To change only a file’s owner, we would supply a username without specifying a group.  To change only the owning group, we would call chown this way:

# chown :sales list

We could also use the chgrp command for this.

Access Control Lists

We have seen that the built-in Linux permissions can define access for 3 classes: a user, a group, and all others.  If we wish to implement a more granular set of permissions, we must turn to Access Control Lists.

# ls -l

-rw-rwxr--+ 1 root root     30 Jun 19 08:12 file

Note the + at the end of the permission string above.  This indicates the presence of an ACL.  We can retrieve an ACL with the getfacl command. 

# ls -ld /test

drwx------. 4 root root 100 Jun 22 10:20 /test

# getfacl /test

getfacl: Removing leading '/' from absolute path names

# file: test

# owner: root

# group: root

user::rwx

group::---

other::---

Above, we can see that the /test directory currently has no extended ACLs applied to it.  The listed permissions in the getfacl output match the permissions provided by ls -l, and there is no + character at the end of the permissions string.  ACLs are set using setfacl which has the following options:

*   -m – modify an ACL
*   -x – remove an ACL entry
*   -b – remove all ACLs for file
*   -R – apply ACL recursively through subdirectories
*   and the permissions string: [d]:u|g|o|m:UID|GID:perms, where:

    *   d – [optional] sets this as default
    *   u, g, o – user, group, other
    *   m – mask, sets effective rights mask (like umask)
    *   UID,GID – who we are affecting
    *   perms – in rwx format

Let’s explore some sample usage:

*   Add a direct user, bob, with full permissions to the directory

    *   # setfacl -m u:bob:rwx /test
*   Add a direct group, sales, with read and write permissions on the directory

    *   # setfacl -m g:sales:rw /test
*   Make the permissions for the sales group part of the default ACL

    *   # setfacl -m d:g:sales:rw /test
*   Set permissions for others to read only

    *   # setfacl -m o::r /test
*   Set the effective rights mask to rw-, thereby masking execute away from bob

    *   # setfacl -m m::rw /test
*   Make the mask part of the default ACL

    *   # setfacl -m d:m::rw /test

The result should look something like this:

# getfacl /test

getfacl: Removing leading '/' from absolute path names

# file: test

# owner: root

# group: root

user::rwx

user:bob:rwx#effective:rw-

group::---

group:sales:rw-

mask::rw-

other::r--

default:user::rwx

default:group::---

default:group:sales:rw-

default:mask::rw-

default:other::r—

Module 6:
Regular Expressions

Linux provides several powerful tools for working with text in files and input streams.  These include grep, sed, and awk which perform decidedly different functions, but the central mechanism for each involves regular expressions (RegEx).

Regular expressions provide the ability to match patterns in text.  This simple description belies the incredible utility of regular expressions.  The first tool to be addressed is grep, which can be used to search through text, match a defined pattern (regular expression), and print the resulting matches.  It uses 3 broad categories of commands to define this pattern:

*   Pattern:  these define the string pattern we are searching for.
*   Anchors:  these define the acceptable position for a matched pattern.
*   Modifiers:  These modify how grep treats the character(s) immediately preceding them.

grep also relies on two types of character interpretations:

*   Literal characters:  characters with no special meaning, i.e. the character a is the literal lowercase alphabetic character a.
*   Metacharacters:  characters with additional meanings beyond the literal, i.e. the dollar sign $ is interpreted as an anchoring metacharacter, translating to “at the end of a line”.

Since grep treats characters as literals or metacharacters situationally, certain characters must be escaped; that is, they must be flipped, depending on the situation, from a literal to a metacharacter or vice versa.  This can lead to regular expressions that look something like this:

'@[a-zA-Z_.]\+\?\.[a-zA-Z]\{2,3\}' .

We will come back to this expression at the end of the module.  For now, notice the backslashes in the string above.  Each of these escapes the character that follows it.  In basic grep, the following characters are treated as literals: + ? | {} ()

If we wish them to be treated as metacharacters, that is to have a special meaning, we must escape them with the backslash: \+ \? \|  \{ \}  \( \)

Extended grep inverts this logic: these characters are metacharacters by default, and must be escaped if we want them treated as literals.  Consider the examples below where -E causes grep to treat the regex as an extended regular expression.  We could also use the egrep, which is equivalent, but deprecated.  When dealing with grep, always be mindful of whether you are using a basic regular expression or an extended regular expression, and apply appropriate escapes as required.

With escapes:

# grep '@[a-zA-Z_.]\+\?\.[a-zA-Z]\{2,3\}' /test/file

tim@honey.net

# grep -E '@[a-zA-Z_.]\+\?\.[a-zA-Z]\{2,3\}' /test/file

###<<< - no results

Without escapes:

# grep -E  '@[a-zA-Z_.]+?\.[a-zA-Z]{2,3}' /test/file

tim@honey.net

# grep '@[a-zA-Z_.]+?\.[a-zA-Z]{2,3}' /test/file

###<<< - no results

Moving beyond the backslashes in the example regular expression, we can see groups of characters like this [a-zA-Z_.]  These are called character sets.  These evaluate to:

*   [a-z]Match any single lowercase alpha character
*   [A-Z]Match any single uppercase alpha character
*   [abc]Match any one of a, b, or c.
*   [0-9]Match any single digit, 0 through 9.
*   [^a2]Match any character which is NOT an “a” or a “2”
*   [.]When enclosed in braces, a literal period. 
*   .A period not enclosed in braces, match any single character other than line break

Return to the example [a-zA-Z_.] This can be interpreted as "any upper or lowercase alphabetic character, or an underscore, or a period." Note that a dot inside of a character set is never interpreted as a metacharacter, but by default a dot outside of a character set will be a metacharacter representing any single character.

Here are some examples of character sets, working with a file called list containing the following text :

red

road

read

radical

The road is radical.

all lowercase

0123456789

123

789

ALL CAPS

To find lines in this file that contain either red OR rad, we would use:

# grep 'r[ea]d' list

red

radical

The road is radical.

Above, grep matched the pattern red OR rad in three lines.  It did not matter if this pattern occurred inside of a larger string.  More interesting, however, is what grep did not match.  Notice that read was not matched, despite containing both the e and the a from the defined character set.  Let’s look at the expression again:  ‘r[ea]d’ This evaluates as
"Match anything that starts with an r, followed by either an e OR an a, followed by a d."

To find lines which contain capital letters, we could do this:

# grep [A-Z] list

The road is radical.

ALL CAPS

Simple enough.  But what if we wanted to find only lines that did NOT contain uppercase letters?  We might try this:

# grep [a-z] list

red

road

read

radical

The road is radical.

all lowercase

This got rid of the ALL CAPS line, but still matched The.  The expression:  [a-z] evaluates as: "Match any lowercase character."  In The road is radical, only the T is not matched.  Every other character was matched, and so the line was returned.  To get lines which did not contain any uppercase characters, use -v to invert the match and return only lines which do not contain the given pattern.

# grep -v [A-Z] list

red

road

read

radical

all lowercase

0123456789

123

789

Suppose we wanted to match capital letters only if they occur at the beginning of a line.  We can’t do this with character sets alone.  To accomplish this, we will need to use anchors.

We can assign desired positions to pattern matches with metacharacters known as anchors.  The dollar sign $ and caret ^ will find matches at the end or beginning of a line respectively.  These are known as anchors. 

To do find all lines that begin with a capital letter, we will place a caret ^ before the pattern we wish to match:

# grep '^[A-Z]' list

The road is radical.

ALL CAPS

To find a pattern at the end of a line, we use the dollar sign $ placed immediately after the pattern we are trying to locate.  To match all lines ending with the lowercase letter “d”:

# grep 'd$' list

red

road

read

Note that anchor characters lose their special meaning if they are not placed at the beginning or end of a pattern.  To explain this, let’s add two lines to our list file and conduct an experiment:

# echo '$1.51' >> list

# echo '$1.52' >> list

# grep '1$' list

$1.51

# grep '$1' list

$1.51

$1.52

In the second example, the anchor was ignored, or, more specifically, was interpreted as a literal.  Any lines containing the character string $1 were returned.

The caret ^ is the anchor for "the beginning of a line" when placed before a pattern.  When placed inside of a character set, it will negate the pattern that follows it.  An example:

# grep '[^0-9]' list

red

road

read

radical

The road is radical.

all lowercase

ALL CAPS

We might have expected this to return any lines beginning with a single digit.  Instead, we have returned all lines which do not contain any digits at all.

There are also some situations in which we may have an idea of what sort of pattern we want to match, but not precisely which variant of that pattern will be returned.  If we wanted to find all instances in which a word was repeated, we might start by creating a pattern that would match any word.  We know it would be composed only of uppercase and lowercase alphabetic characters.  A set to match any single character like that might look like this:  [a-zA-z]

The problem now is that we have no idea how long a word might be.  It would be at least one character long, but could be composed of many.  We have a way to address this:  [a-zA-Z]+

This will match any string composed of one or more alpha characters.  The plus sign (+) functions as a modifier; it specifies how many time a given pattern must be matched to return a result.  We will return to modifiers in a moment.  For now, we need only understand that the plus sign evaluates as “match the preceding pattern one or more times”.  In other words, a match for the pattern we’re working with would be “one or more alphabetic characters in sequence”.

To tell grep that we want to find this pattern ONLY when it repeats we need to introduce a new concept: backreferences.  A backreference allows regular expressions to store a match and refer to it later.  To create a stored pattern, we simply surround the match criteria with parenthesis:  ([a-zA-Z]+)

We can store up to nine backreferences in a single expression, and call them with a backslash, followed by a number (1 through 9, based on order of occurrence).  To practice this, let’s create a small file and run our test pattern against it:

[root@ELG-6 lab]# grep -E '([a-zA-Z]+)' testfile

the the

the these

there thesis

the thesis

there there

one one one

This returns the entire contents of the file (though it wouldn’t have matched any lines containing only numbers, if they had been present).  To match repetition, we’ll tell grep to match the pattern, store it at /1, and then try to match that pattern again immediately following a space:

[root@ELG-6 lab]# grep -E '([a-zA-Z]+) \1' testfile

the the

the these

the thesis

there there

one one one

This is close, but we have some odd behaviors.  In the second and third lines the stored pattern was matched inside of a longer string.  This isn’t exactly the desired behavior.  To fix this, we need to tell grep to respect word barriers.  We can do this by using less than < and greater than >, but we’ll need to escape them.

[root@ELG-6 lab]# grep -E '(\<[a-zA-Z]+\>) \<\1\>' testfile

the the

there there

one one one

Now we have it.  If you’re concerned about the last line, remember that grep returns entire lines by default.  If you only want the matched text, try using the -o option, like this:

[root@ELG-6 lab]# grep -oE '(\<[a-zA-Z]+\>) \<\1\>' testfile

the the

there there

one one

We may also use alternation. Alternation allows us to specify multiple possible patterns, only one of which must be matched to return a result.  The metacharacter for alternation is the pipe | which may be read as OR.  To match lines beginning with r OR ending with 3:

# grep -E '^r|3$' list

red

road

read

radical

123

Here we used -E to avoid having to escape the pipe metacharacter.

Returning to modifiers, we may modify how often a pattern must be matched in order for grep to return it.  These characters are modifiers:

*   ?Match the preceding 0 or 1 times
*   *Match the preceding 0 or more times
*   +Match the preceding 1 or more times
*   {N}Match the preceding exactly N times
*   {N,}Match the preceding N or more times
*   {N,M}Match the preceding between N and M times

Let’s try pulling some numeric strings out of our target file.  This evaluates as "Return any line in which a digit, 0 through 9, occurs at least once."

# grep -E '[0-9]+' list

0123456789

123

789

This evaluates as "Return any line containing a sequence of 3 digits, 0 through 9."

# grep -E '[0-9]{3}' list

0123456789

123

789

This evaluates as "Return any line containing a sequence of 4 digits, 0 through 9."

# grep -E '[0-9]{4}' list

0123456789

If we had want to return lines containing only a 3-digit number, and nothing else, there are two solutions. One way is to use anchors and modifiers, like this:

# grep -E '^[0-9]{3}$' list

123

789

This instructs grep to return lines in which:

*   ^The line begins, and then
*   [0-9]{3}3 digits (0 through 9) appear in sequence, and then
*   $the line ends.

We could also use the -x option, which instructs grep to match the given pattern against entire lines, rather than finding the pattern within a line:

# grep -x '[0-9]\{3\}' list

123

789

Taking another look

Let’s take another look at the expression we introduced at the beginning of this module.

'@[a-zA-Z_.]\+\?\.[a-zA-Z]\{2,3\}'

We should be able to break it down now:

*   @a literal @ symbol
*   [a-zA-Z_.]any lowercase or uppercase alpha character, an underscore, OR a period
*   \+match the preceding expression at least once
*   \?match the preceding expression no more than once
*   \.A literal dot, “.”
*   [a-zA-Z]Any alpha character, upper or lowercase
*   \{2,3\}match the preceding either 2 or 3 times; no more, no less

Here is a new file to consider:

tim@honey.pot.not

tim@honot.not

tim@sonot.au

tim@bonnot

tim.turner

tim.turner@bon_ney.con

@kim.com

a@b.c

*   Which of these lines will be matched?  Which won’t, and why?
*   What sort of patterns could we place before the @ symbol?
*   Can you think of other ways to achieve the same goals? 
*   Can you improve readability by eliminating the need to escape some of the characters?

sed

The man pages for sed and awk describe them as follows:

*   sed – stream editor for filtering and transforming text
*   awk – pattern scanning and processing language.  On EL6 this is linked to /bin/gawk.

Both make use of regular expressions, and both are complex enough that entire books have been written regarding their usage.  We cannot, and will not attempt to, cover these utilities comprehensively. Instead, we will focus on some of the more pedestrian uses of each – commands of value to system administrators.

The basic invocation of sed is as follows sed options  commands  file.  The options alter the standard behavior of sed; the commands define what sed will do.

To understand why sed does things the way it does, we must first consider sed’s standard behavior.  Without options, sed will do the following:

*   Read the first line of input into the pattern space (sed’s workspace buffer)
*   Perform the commands from the commands section
*   Print the contents of the buffer to output
*   Clear the buffer
*   Read the next line of input into the buffer

We can demonstrate this process by calling sed without commands against a file (we’ll use a modified copy of our hosts file as a target):

# sed '' hosts

192.168.1.166      example-svr      example-svr.example.not

192.168.1.165      example-clnt     example-client.example.not

Above, sed performed its standard behavior by reading in the first line, doing nothing, printing the line to STDOUT, clearing the buffer, and repeating the behavior.

If this description of sed’s behavior seems unnecessary, consider the following: there is a command, p,  which explicitly instructs sed to print whatever is currently in the working buffer to output.  We know that, as part of its standard behavior, sed will already print the contents of the buffer after running any specified commands.  The result?  See below:

# sed 'p' hosts

192.168.1.166      example-svr      example-svr.example.not

192.168.1.166      example-svr      example-svr.example.not

192.168.1.165      example-clnt     example-client.example.not

192.168.1.165      example-clnt     example-client.example.not

Each line was printed twice.  We could suppress the automatic printing step from the standard behavior with an option, -n.  Let’s try it:

# sed -n 'p' hosts

192.168.1.166      example-svr      example-svr.example.not

192.168.1.165      example-clnt     example-client.example.not

Keep in mind that sed will perform any commands listed in the commands section in order, from left to right.  Let’s put multiple commands into a single statement using the semicolon as a separator.

# sed 'p;s/example/CHANGED/' hosts

192.168.1.166      example-svr      example-svr.example.not

192.168.1.166      CHANGED-svr      example-svr.example.not

192.168.1.165      example-clnt     example-client.example.not

192.168.1.165      CHANGED-clnt     example-client.example.not

Walking through the steps, sed:

*   Reads a line into the buffer.
*   Performs the command p:  print the unmodified line.
*   Performs the command s, substituting the first instance of example with CHANGED.
*   Finishes its work on the line and prints the results
*   Clears the buffer
*   Repeats, reading the next line into the buffer.

Armed with this understanding, we can move on to a discussion of sed’s more obvious uses.

Perhaps the most common use for sed is performing simple pattern substitution; that is, finding a string and replacing it with something else.  This is what was done with the earlier command 's/example/CHANGED/'.

Let’s take a closer look.

# cat hosts

192.168.1.166      example-svr      example-svr.example.not

192.168.1.165      example-clnt     example-client.example.not

# sed 's/example/production/' hosts

192.168.1.166     production-svr      example-svr.example.not

192.168.1.165      production-clnt     example-client.example.not

Above, sed substituted the word production for example.  It will do this once per line unless directed otherwise.  A g at the end of a command directs sed to perform the action 'globally':

# sed 's/example/production/g' hosts

192.168.1.166     production-svr      production-svr.production.not

192.168.1.165     production-clnt     production-client.production.not

Let’s break this command down:

*   ssubstitute
*   /delimiter (or separator)
*   examplewhat we want to replace
*   /delimiter
*   productionwhat we want to replace it with
*   /delimiter
*   gglobally – where to make the substitution in the line

To save the results, use command line redirection (> or >>) to a file.  To get sed to save its changes in the source file, use the -i option (in-place edit).

We might also like sed to replace patterns based on regular expressions rather than literal character strings.  To test this, let’s first make some alterations to our text file:

# sed -i 's/example/production/' hosts

# cat hosts

192.168.1.166      production-svr      example-svr.example.not

192.168.1.165      production-clnt     example-client.example.not

Let’s suppose we wish to accomplish two things: replace all remaining instances of “example” in the hostname portion only with “production”, and replace all dashes with underscores.  Here’s one way to do this:

# sed 's/\(production\|example\)-/production_/g' hosts

192.168.1.166      production_svr      production_svr.example.not

192.168.1.165      production_clnt     production_client.example.not

Breaking it down:

*   s – substitute
*   / – delimiter
*   \(production\|example\) – match production or example, escaping metacharacters
*   - – where production or example are followed by a literal dash
*   / – delimiter
*   production_ – replace the matched items with this string
*   / – delimiter
*   g – global replacement

A couple of notes regarding sed  

The ampersand & has a special meaning in sed:  it corresponds to a previously matched pattern.  grep allowed matched patterns to be stored using numeric backreferences 1-9.  sed accepts these, and adds & for use in the replacement section of a substitution command. 

Consider the following example text:

1-2-3

1.2.3

1:2:3

If we wished to double the dashes, dots, and colons, we could do it by using &, like this:

# sed 's/[.\:-]/&&/g' <testfile

1--2--3

1..2..3

1::2::3

Note that parentheses were not required to use the ampersand.  Also note, when using a hyphen in a character set, that the hyphen should be placed last in the list so that it is not interpreted as part of a range.

As a final thought, we would like to point out that the use of forward slashes as delimiters (or separators) in sed is by convention only.  Really, any character that follows the “s” in the substitution command can be used as a separator.  This is also a valid sed expression, using pipe | as a delimiter:

sed 's|[.\:-]|&&|g' <testfile

1--2--3

1..2..3

1::2::3

sed is a powerful tool, and the uses of it go far beyond what is covered in this material.  We encourage students to further explore sed if the opportunity presents itself; it can yield tremendous amounts of utility.

awk

Although awk usage can be tremendously complex, there are times when simple invocations of awk are the best tool for accomplishing a particular task.  In this section, we will briefly discuss how awk treats files, then proceed to a series of small examples with accompanying explanation.

awk sees files as a series of records and fields, which it reviews one line at a time.  The default field separator is whitespace, and the default record separator is a linefeed.  Consider this:

Apple $1.95

Pear $0.57

Strawberry $1.26

By default, awk would see this as a set of 3 records, with 2 fields each:

# awk 'BEGIN { print "Record and Fields of:" } \

{if(NR == 1) { print FILENAME }; } \

END { print "\n""Num Recs:\t",NR,"\n""Num Fields:\t",NF }' pfile

Record and Fields of:

pfile

Num Recs:        3

Num Fields:      2

Here we have intentionally chosen a more complex invocation of awk.  Throughout the remainder of this module, we will cover the individual components that make this work.  We will work through a series of simple examples, and then return to an interpretation of the more complex set above.

To begin, let’s suppose we only wanted the information from the first field in our file (the fruit names).  We could ask awk to print them in this way:

# awk '{ print $1 }' pfile

Apple

Pear

Strawberry

$1, in this case, is a built-in variable that awk understands as “the first field”.  We could print the second field with $2.  $0 is the entire line, and $NF (Number of Fields) functions here as a shortcut to the last field:

# awk '{ print $0 }' pfile

Apple $1.95

Pear $0.57

Strawberry $1.26

# awk '{ print $NF }' pfile

$1.95

$0.57

$1.26

We can also redefine the field separator from whitespace to something else.  Let’s try this with /etc/passwd:

# awk -F: '/1[0-9][0-9][0-9]/ { print $1,$3 }' /etc/passwd

Lisa 1003

caroline 1004

lori 1005

bob 1006

ldapuser1 1007

ldapuser2 1008

Let's break that down:

*   -F:set field separator to colon
*   /1[0-9][0-9][0-9]/match this pattern (it’s a regex!)
*   { print $1,$3 }print fields 1 and 3

There’s another way to set the field separator, and it involves the BEGIN section of an awk  program.  We can write awk  programs in three main sections:

*   BEGIN – We run these lines first.  Often used to make header or set variables.
*   BODY – Typically where we put the bulk of our work.
*   END – Runs these lines last.  Often used to create a footer.

We can write awk programs as if they were shell scripts.  Here is one called awkish:

#!/bin/gawk -f

BEGIN { print "Record and Fields of:" }

{ if(NR == 1) { print FILENAME }; }

END { print "\n""Num Recs:\t",NR,"\n""Num Fields:\t",NF }

Running that gets us this:

# /awkish pfile

Record and Fields of:

pfile

Num Recs:        3

Num Fields:      2

In the script, we specified a program which should be used to interpret our commands:
#! /bin/gawk -f.  The -f option tells it to expect a file as an argument.  We passed it pfile at runtime, which uses whitespace as a record separator.  What would happen if we had passed it something like /etc/group instead?

# /awkish /etc/group

Record and Fields of:

/etc/group

Num Recs:        88

Num Fields:      1

One field?  Let’s use awk and sed to get the first line out of that file so we can take a closer look.

# awk 'NR==1 { print }' /etc/group

root:x:0:

# sed -n '1p' /etc/group

root:x:0:

Human eyes would register at least 3 fields here (technically four – the last field is just empty).  We’ve used -F to set the separator to a colon earlier; this time, let’s declare it in the BEGIN section of our awk script.

BEGIN { FS=":";print "Record and Fields of:" }

We added FS=":"; to the BEGIN section of our script.  This sets the Field Separator to a colon.  Running it again:

# /awkish /etc/group

Record and Fields of:

/etc/group

Num Recs:        88

Num Fields:      4

As used above, FS and NR are built-in variables that awk populates based on what it knows about a file.  Here’s a short list of the more commonly used ones:

*   FILENAME– the name of the input file; undefined in BEGIN block
*   FS/RS – input field separator/record separator
*   OFS/ORS– output field separator/record separator
*   NF– number of fields in current record
*   NR – number of current record
*   FNR – if multiple input files, record number of current file
*   $0 – entire current record
*   $n – where n is a number; field by sequence e.g. $1,$2

With what we’ve discussed so far, we’re almost ready to return to the “complex” awk example from the beginning of this section.  There is, however, one concept yet remaining – conditional statements (specifically, if).  Let’s reexamine a line from the body section of our awk script.

{ if(NR == 1) { print FILENAME }; }

In the above example, the outer curly braces simply represent the BODY of the script and the semicolon ends the line.  We may disregard them for the moment and break down the remainder:

if( condition  ) { action };

As a condition we used NR==1.  NR is a variable which holds the current record number.  The double equal signs == are interpreted as “is equal to”.  In other words, the statement reads:  “if we are currently evaluating the first record of the file”.  Our action was print FILENAME.  When the script executed, the filename was printed exactly once – when we evaluated the first record.

Returning to our original example:

# awk 'BEGIN { print "Record and Fields of:" } \

{if(NR == 1) { print FILENAME }; } \

END { print "\n""Num Recs:\t",NR,"\n""Num Fields:\t",NF }' pfile

At this point, the only questions remaining should be:
Why are there backslashes on the ends of the lines?  And, what’s with the “\n” and “\t”?

Consider this example, using echo instead of awk: 

# echo \

$'\n'hi$'\t'there

hi      there

The backslash at the end of the line is used for line continuation in bash.  We would use it if a command was exceedingly long, mainly for clarity in reading.

The \n represents a newline, and the \t represents a horizontal tab.  It makes the commands easier to parse, and it made the output prettier.

Making substitutions with awk

To this point, we’ve used awk in a similar fashion to grep.  Now we’ll bend it to a purpose more like that of sed.

We can use awk to perform substitutions, and, as with sed, we can specify whether we wish those substitutions to be made once per line (record) or globally within a line.  To do this, we will use two functions built into awk: sub and gsub.

Returning to a previous example file, we can demonstrate these functions by replacing the sting “the” with the string “THE”:

# awk '{ sub(/the/,"THE"); print }' regtest

THE the

THE these

THEre thesis

THE thesis

THEre there

one one one

Breaking it down, we see:

awk ‘{ }’the invocation of awk and the braces containing the program

sub( )the substitution function (one replacement per record)

/the/,the pattern we are searching for, comma is a delimiter

“THE”what to replace matched patterns with

; printsemicolon separates commands, print prints to STDOUT

regtestthe input file

To replace all matches, rather than a single match per record, we could instead use the gsub function, as follows:

[root@ELG-6 lab]# awk '{ gsub(/the/,"THE"); print }' regtest

THE THE

THE THEse

THEre THEsis

THE THEsis

THEre THEre

one one one

The invocation for the two functions is identical, but we can now see that all matches have been replaced, as desired.                            

Module 7:
File Systems

File systems provide us with methods for organizing, structuring, and accounting for files on a device.  “Device” in this case could be a disk, a partition, a logical volume, or any number of other data-holding things. 

Though there is tremendous variation in the way that file systems treat data, most modern file systems share some common concepts.  Among these are:

*   Blocks -- the smallest chunk of space that a file system can track.  Each block will have a unique number assigned to it by the file system.  All data written to a file system must ultimately be stored at one or more of these blocks.
*   Superblocks – a special type of block that contains information about the file system itself (file system type, size, available inodes, free space, etc).  When utilities like mkfs.ext4 write the file system structure to a device, the superblock will be created in one of the first blocks in that space.  Backup copies of the superblock may be created later, and spread throughout the addressable space at the file system’s discretion.
*   Inodes – also stored in a special space.  Inodes do most of the heavy lifting in file systems, and contain metadata about file characteristics and pointers to the blocks holding the data of files.
*   Directory blocks – provide a way to associate file names with inodes.  An entry could be as simple as: 27199300 file.  In this case, the inode number 27199300 is associated with the filename “file”.
*   Data blocks – where data is actually stored.  For example, if a user created a small text file, the data blocks would hold the text entered into the file by the user.  Everything else, including the name of the file, would be metadata.  As discussed later, data blocks can be either direct or indirect.

Inodes

Inodes are integral to file system function.  Each inode will contain information about a file or directory (ex. permissions, timestamps, size, etc.).  We call this information “metadata”; data about data.  Interestingly, file inodes do not contain a file’s name.  To understand why that is, we must briefly explore how files are retrieved when a user requests them.

Let’s begin in the /test directory of the example server:

# ls -i

17157383 1          27199300 file     27204151 pathfile

27204150 binary     27204148 link     27204152 source

9057104 directory  27124462 outfile  913922 inode.example

Here, we’ve executed the ls command with the -i option.  This instructs ls to list the inode number associated with a directory entry.  We’ve highlighted the entry for a file called inode.example.  Note the number 913922.  This is the index number of the inode associated with that filename.

Earlier, we discussed pathing.  The absolute path to the inode.example file would be:

/test/inode.example

The first directory listed in this path is root (/).  This is followed by the test directory, and finally by the file, inode.example.

Suppose we wish to retrieve the contents of inode.example and display them.

# cat /test/inode.example

These are the contents of the inode.example file.

This attempt was successful, but to locate the data blocks containing the contents of inode.example, the system had to begin at root (/) and proceed from there.

Ordinarily, to find the inode of a given file, a directory listing would be consulted (as we saw at the beginning of this section).  The root directory, however, is at the top of the hierarchy.  No directory exists that contains an entry for it.  There is no procedural way to deduce the location of the inode.  Because of this, the inode for the root file system will always exist at a known location.  Traditionally, this has been index "2", and for ext4 file systems (the default in EL6), it still is:

# ls -id /

2 /

However, for reasons that are far beyond the scope of this text, it sometimes isn’t.  On an example EL7 server, the root file system was built on a logical volume and formatted with XFS.  The root inode here is 64, which was determined by examining the superblock of the file system:

# xfs_db -r /dev/mapper/cl-root

xfs_db> sb

xfs_db> p

magicnum = 0x58465342

blocksize = 4096

dblocks = 3511296

rblocks = 0

rextents = 0

uuid = 339f049b-b247-4316-9b49-f1f3f597c73f

logstart = 2097156

rootino = 64

XFS is the default file system type for RHEL 7 (at the time of this writing).  We encourage further exploration of its capabilities and eccentricities as time allows.

Returning to our exercise, we can now definitively state that the path to inode.example begins at inode 2.  Let’s take a closer look:

# stat /

File: `/'

Size: 4096            Blocks: 8          IO Block: 4096   directory

Device: fd00h/64768d    Inode: 2           Links: 26

Access: (0555/dr-xr-xr-x)  Uid: (    0/    root)   Gid: (    0/    root)

Access: 2017-07-24 09:52:52.691988591 -0500

Modify: 2017-07-25 10:47:47.619708962 -0500

Change: 2017-07-25 10:47:47.619708962 -0500

Here we can see that this file is named "/", and that it is a directory.  We can see the size, inode number, permissions and ownership, and a few other interesting details. 

Take note of this line:

Access: (0555/dr-xr-xr-x)

We'll take a much closer look at this later, but for now, it's enough to know that this string represents file level permissions. 

To retrieve inode.example, the system first retrieved the inode for the root directory.  Then it checked the permission string to see if the invoking user had been granted access to the file.  In this case, read permission was allowed.  The next item in the requested path was test, another directory. 

To find the inode for test, the contents of / were examined:

# ls -i /

118 bin   16961581 iso           1 proc     913921 test

64 boot       121 lib    16797761 root     8388680 tmp

... truncated ..

From here the process was repeated: check access, consult directories, find inode, retrieve contents.

Ultimately, we arrived at the final item in our path, the inode.example file.

# ls -i

913923 1            913925 directory      913922 inode.example

913928 outfile      913930 source         913924 binary   

913926 file         913927 link           913929 pathfile

A final access check was performed.  It succeeded.  The inode pointed the way to the data blocks for inode.example, the data was retrieved, and the requested functions were performed against it.  In our case, we simply wanted the contents listed to STDOUT.  cat performed this function, resulting in the following:

# cat inode.example

These are the contents of the inode.example file.

Throughout our traversal of the file system, only one piece of information could be considered data.  It is this sentence:

These are the contents of the inode.example file.

Everything else along the way was metadata, including the directories and even the name of the file. 

Hard Links

To understand links, it may help to begin with the idea that files don't have names – at least not as we classically understand them.  Instead, they have locations (data blocks, pointed to by inodes), and labels by which their inodes can be referenced.  These labels provide the same function as a name, but in reality, they are simply a mechanism for resolving down to an inode number.  Files exist at a location, and will continue to do so no matter what they may be called, or by how many names they are known.

Consider the following:

# ls -l

total 4

-rw-r--r--. 1 root root 124 Jun 16 08:35 inode.example

Notice the number "1" after the permission string.  This is what's known as a "link count".  

Here’s another listing:

# ls -i

913922 inode.example

Above, we see the same directory listing, now with inodes.  Note the inode number: 913922  The link count from before indicated that this inode was referenced by 1 label.  In this case, that label was inode.example.

# ln inode.example newfile

# ls -i

913922 inode.example  913922 newfile

Above, we used the ln command to create a hard link from inode.example to newfile. The directory listing indicates that both files now exist in the directory.  A closer inspection, however, reveals that the inode numbers are the same for both files. 

# ls -l

total 8

-rw-r--r--. 2 root root 124 Jun 16 08:35 inode.example

-rw-r--r--. 2 root root 124 Jun 16 08:35 newfile

Again, we appear to have two files, but the information for each is identical.  Only the filenames differ.  Notice also that the link count for each is now 2.  inode.example and newfile are in fact the same file, referenced by different names.  Modifying one has the apparent effect of modifying the other as well.  Deleting one, however, will not cause the other to disappear.  Instead, the link count will simply decrement by one and the directory entry for the deleted “file” will disappear.  When link count reaches zero, a file is effectively destroyed.

# ls -l

total 8

-rw-r--r--. 2 root root 124 Jun 16 08:35 inode.example

-rw-r--r--. 2 root root 124 Jun 16 08:35 newfile

# /usr/bin/rm inode.example

# ls -l

total 4

-rw-r--r--. 1 root root 124 Jun 16 08:35 newfile

# cat newfile

These are the contents of the inode.example file.

The directory listing above shows two files.  The /usr/bin/rm command was used to remove the "original" file, inode.example.  Another listing shows only newfile, now with a link count of 1.  The cat command was then invoked to display the contents of newfile returning this:

These are the contents of the inode.example file.

This demonstrates that hard links do not create new files as we understand them.  Instead, they create additional directory listings for existing files.

Hard links are useful, but they have limitations.  Foremost amongst these is that they may not cross file system boundaries.  We would not expect inode 103 in file system FOO to contain the contents of inode 103 in file system BAR.  This is because inode numbers are used by a file system to keep track of its own contents, not the contents of other systems.  There is a way to reference, through a link, the contents of an inode on another file system.  This type of link is called a "symbolic" link. 

Symbolic Links

Symbolic links are files whose contents consist only of a pointer to some other file.  We can create one in this fashion:

ln -s /path/to/original /path/to/created/link

Let’s use this to "recreate" the inode.example file from the last section:

# ls

newfile

# ln -s /test/itest/newfile /inode.example

# ls -l

total 4

lrwxrwxrwx. 1 root root  19 Jun 16 11:20 inode.example -> /test/itest/newfile

-rw-r--r--. 1 root root 124 Jun 16 08:35 newfile

In the above example, we used ln -s to create a symbolic link called inode.example (which points to newfile in the same directory).  Look closely at this part of the output:

inode.example -> /test/itest/newfile

This string indicates that inode.example, when referenced, will attempt to return /test/itest/newfile instead.  Let’s try a different listing:

# ls -i

27228260 inode.example  913922 newfile

Notice that the inode numbers are different.  Unlike hard links, symbolic links do not refer to an inode directly.  They must not; if they did, they could not cross file system boundaries.  For this reason, a new inode is created, but only contains a pointer (via a simple path) to resources elsewhere on the system.

One interesting consequence of this behavior is that, should we now choose to delete newfile, inode.example will still exist (it is tracked by a separate inode). 

Attempts to read the contents of inode.example would fail, returning an error:  No such file or directory

If we were to then create another file called newfile and store it in the same location as the original, the link would again function – though it would now point to an entirely different file.

Creating file systems

To create a file system, a device must exist onto which the file system may be placed.  Although certain types of file systems may exist purely in RAM, we will focus on disk-based implementations.  To see a list of available hard disks, we could use lsblk:

# lsblk

NAME                         MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT

sda                            8:0    0   40G  0 disk

├─sda1                         8:1    0  500M  0 part /boot

└─sda2                         8:2    0 39.5G  0 part

├─vg_server-lv_root (dm-0) 253:0    0 35.6G  0 lvm  /

└─vg_server-lv_swap (dm-1) 253:1    0    4G  0 lvm  [SWAP]

sr0                           11:0    1 1024M  0 rom

sdb                            8:16   0   10G  0 disk

└─sdb1                         8:17   0    1G  0 part

In the highlighted portions of the output above, we can see a listing for two hard drives and their partitions.  These are: sda (parts sda1,sda2) and sdb (parts sdb1).  You may read this as:

sdscsi disk

a/bdisk order, alphabetical (a=1st drive, b=2nd, etc.)

1/2partition number

Drive sdb only has a single partition, sdb1.  It looks like we have some space free on the device.  Let’s verify that with fdisk -l (remember: devices live in the /dev directory!):

# fdisk -l /dev/sdb

Disk /dev/sdb: 10.7 GB, 10737418240 bytes

64 heads, 32 sectors/track, 10240 cylinders

Units = cylinders of 2048 * 512 = 1048576 bytes

Sector size (logical/physical): 512 bytes / 512 bytes

I/O size (minimum/optimal): 512 bytes / 512 bytes

Disk identifier: 0x2c994a74

Device Boot      Start         End      Blocks   Id  System

/dev/sdb1               1        1025     1049584   83  Linux

The above output confirms that free space is available.  This was determined by subtracting the partitioned block count and size from the device size.  This information can be more directly found using
parted /dev/sdb, followed by print free.

Let’s walk through the creation of a new 1 GB partition (using fdisk).  To create a new partition here, call fdisk /dev/sdb.  Note that changes made in this program do not take effect until the w (write) option is selected.  If at any point, you feel as if you have made a mistake in this program, immediately press q (quit) to exit without saving.  Pressing m shows a menu of available commands, n creates a new partition, and p will print the partition table as below (showing that we have only one partition):

Command (m for help): p

Disk /dev/sdb: 10.7 GB, 10737418240 bytes

64 heads, 32 sectors/track, 10240 cylinders, total 20971520 sectors

Units = sectors of 1 * 512 = 512 bytes

Sector size (logical/physical): 512 bytes / 512 bytes

I/O size (minimum/optimal): 512 bytes / 512 bytes

Disk identifier: 0x2c994a74

Device Boot      Start         End      Blocks   Id  System

/dev/sdb1              32     2099199     1049584   83  Linux

Next, we will choose n(new) to create a new partition.  User input is bolded.

Command (m for help): n

Command action

e   extended

p   primary partition (1-4)

p

Partition number (1-4): 2

First sector (2099200-20971519, default 2099200): <enter>

Using default value 2099200

Last sector, +sectors or +size{K,M,G} (2099200-20971519, default 20971519): +1G

Command (m for help): p

Disk /dev/sdb: 8589 MB, 8589934592 bytes, 16777216 sectors

Units = sectors of 1 * 512 = 512 bytes

Sector size (logical/physical): 512 bytes / 512 bytes

I/O size (minimum/optimal): 512 bytes / 512 bytes

Disk label type: dos

Disk identifier: 0x61b3cd4c

Device Boot      Start         End      Blocks   Id  System

/dev/sdb1            2048     2099199     1048576   83  Linux

/dev/sdb2         2099200     4196351     1048576   83  Linux

Command (m for help): w

The partition table has been altered!

Calling ioctl() to re-read partition table.

Syncing disks.

We have now created a new 1GiB partition.  We listed the partition table to verify our work, then wrote the table to disk.  This can be verified with lsblk, or with cat /proc/partitions.

# lsblk

NAME                         MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT

sda                            8:0    0   40G  0 disk

├─sda1                         8:1    0  500M  0 part /boot

└─sda2                         8:2    0 39.5G  0 part

├─vg_server-lv_root (dm-0) 253:0    0 35.6G  0 lvm  /

└─vg_server-lv_swap (dm-1) 253:1    0    4G  0 lvm  [SWAP]

sr0                           11:0    1 1024M  0 rom

sdb                            8:16   0   10G  0 disk

├─sdb1                         8:17   0    1G  0 part

└─sdb2                         8:18   0    1G  0 part

If our changes were not reflected here, we could manually inform the kernel of the changes using partprobe.

Making the file system

EL6 offers support for several file systems.  Tools for creating these are supplied to us in /sbin:

#ls /sbin/mkfs*

/sbin/mkfs         /sbin/mkfs.ext2  /sbin/mkfs.ext4  /sbin/mkfs.msdos

/sbin/mkfs.cramfs  /sbin/mkfs.ext3 /sbin/mkfs.ext4dev /sbin/mkfs.vfat

These commands may be used to create a file system of the type specified in their extension.  For this example, we’ll be working with ext4.  From our earlier work, we know that a free partition exists at /dev/sdb2.  Let’s use mkfs.ext4 to format /dev/sdb2.

# mkfs.ext4 -L ext4.example /dev/sdb2

mke2fs 1.41.12 (17-May-2010)

File system label=ext4.example

OS type: Linux

Block size=4096 (log=2)

Fragment size=4096 (log=2)

Stride=0 blocks, Stripe width=0 blocks

65536 inodes, 262144 blocks

13107 blocks (5.00%) reserved for the super user

First data block=0

Maximum file system blocks=268435456

8 block groups

32768 blocks per group, 32768 fragments per group

8192 inodes per group

Superblock backups stored on blocks:

32768, 98304, 163840, 229376

Writing inode tables: done

Creating journal (8192 blocks): done

Writing superblocks and file system accounting information: done

Many other options could have been supplied here, but the job is done.  An ext4 file system has now been created on/dev/sdb2. 

mount

In the previous section, we created an ext4 file system on /dev/sdb2.  When we did so, the data structures necessary for that file system to track data blocks for its files and directories were established.  However, these files and directories are inaccessible to us.  This is because we inhabit the root file system.  The root file system, like any other, maintains an inode table and directory structure.

How can the root file system possibly know, by consulting its own data structures, what is inside the file system at /dev/sdb2?  The answer is:  it can’t.  The contents of that file system exist on the device, but we don’t know how to reach them.  Root (/) simply doesn’t have a map to that location.

We can solve this problem through a process called mounting. Mounting allows us to make a file system available via a directory (also called a mount point) in the root file system.  After the mounting operation occurs, any calls for the contents of the mount point directory will return the top level of the mounted file system (instead of the original contents in root).

Let’s explore the concept with a small example.  Here are the contents of a directory called /testmount on the example server.

# ls -l /testmount

total 4

-rw-r--r--. 1 root root 67 Jun 19 14:14 NOTmounted

# cat /testmount/NOTmounted

this file lives in the /testmount directory in the root file system

Note that a single file is present in this directory.  Now we will mount the /dev/sdb2 file system to the /testmount directory.

# mount /dev/sdb2 /testmount

# ls -l /testmount

total 16

drwx------. 2 root root 16384 Jun 19 11:42 lost+found

The file from earlier is gone, and a directory, lost+found, has taken its place.  This is because we are now viewing the contents of the mounted file system instead of the original contents of the /testmount directory.  Essentially, the mount operation tells the kernel to take a detour at the /testmount directory, flipping over to the file system at /dev/sdb2 instead. 

We can unmount the file system to reverse this.

# umount /testmount

# ls -l /testmount

total 4

-rw-r--r--. 1 root root 67 Jun 19 14:14 NOTmounted

Our file is now back. 

Options exist to control the behavior and mode of mounted file systems.  These are passed using mount -o.  Some of the most common mounting options include:

*   defaults – Provides an alias for async,auto,dev,exec,nouser,rw,suid
*   async – Allow the asynchronous input/output operations
*   auto  – Allow the file system to be mounted automatically using mount -a
*   noauto – Disallow automatic mount of the file system using mount -a (default)
*   dev   – Interpret character or block special devices on the file system
*   exec  – Allow the execution of binary files on file system
*   noexec – Disallow the execution of binary files on file system
*   user  –  Allow an ordinary user (non-root) to mount and unmount the file system
*   nouser – Disallow non-root to mount and unmount
*   rw   – Mount read / write
*   ro   – Mount read only
*   suid  – Allow set-user/group bits to take effect.
*   loop  – Mount an image as a loop device
*   remount – Remount the file system in case it is already mounted.

fstab

In the previous section we discussed the concepts behind mounting, and manually mounting and unmounting file systems.  Manual mounts, however, are non-persistent.  They will not automatically be mounted at boot time.  One method of automatic mounting is with autofs, which is prohibited by STIG.  The other uses the file /etc/fstab.  Here is a line from that file and its explanation:

/dev/mapper/vg_server-lv_root/ext4 defaults 1 1

*   /dev/mapper/vg_server-lv_root – what to mount
*   / – where to mount it
*   ext4 – file system type
*   defaults – options (defaults = rw,suid,dev,exec,auto,nouser,async)
*   1 – dump? (1=yes; 0=no)
*   1 – fsck? (1=yes,chk 1st; 2=yes,chk 2nd; 0=do not fsck)

To mount our new file system add a line to fstab:

/dev/sdb2/testmountext4defaults0   0

With this done, we should now be able to mount the file system and verify success using mount.

# mount /testmount

# mount

/dev/mapper/vg_server-lv_root on / type ext4 (rw)

<truncated>

/dev/sdb2 on /testmount type ext4 (rw)

This file system will now be mounted automatically at boot time, along with all other file systems listed in /etc/fstab.

swap

If we require additional swap space on an EL6 system, we may designate either a file or a disk/partition for use as swap.  Below, we explore each of these possibilities in turn.

To create new swap space on a disk or partition, begin by listing available disk space.

# lsblk

NAME                           MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT

sda                              8:0    0   40G  0 disk

├─sda1                           8:1    0  500M  0 part /boot

└─sda2                           8:2    0 39.5G  0 part

├─vg_server-lv_root (dm-0)   253:0    0 35.6G  0 lvm  /

└─vg_server-lv_swap (dm-1)   253:1    0    4G  0 lvm  [SWAP]

sdb                              8:16   0   10G  0 disk

├─sdb1                           8:17   0    1G  0 part

├─sdb2                           8:18   0    1G  0 part /testmount

├─sdb3                           8:19   0    1G  0 part

│ └─ExampleVG-ExampleLV (dm-2) 253:2    0  1.5G  0 lvm

└─sdb4                           8:20   0    1G  0 part

└─ExampleVG-ExampleLV (dm-2) 253:2    0  1.5G  0 lvm

sr0                             11:0    1 1024M  0 rom

We have a free partition in /dev/sdb1.  We will use that as our new swap partition. First, we’ll take a look at our currently available swap space:

# free -m

total       used       free     shared    buffers     cached

Mem:          1893       1266        627          8         45        818

-/+ buffers/cache:        401       1491

Swap:         4063          0       4063

# swapon -s

Filename                                Type            Size    Used    Priority

/dev/dm-1                               partition       4161532 0       -1

Above, the free -m command informs us that we have 4063 MB of free swap space.  We’ll make a note of that.  The swapon -s command tells us that our currently assigned swap locations consist solely of /dev/dm-1.  To use /dev/sdb1 as an additional swap partition, we’ll need to use the mkswap command to set up the partition for swapping:

# mkswap /dev/sdb1

Setting up swapspace version 1, size = 1049580 KiB

no label, UUID=f14f95d0-7c99-456a-939f-46792aa07841

With this done, we need to edit /etc/fstab so that our new swap space will be mounted at boot.  Specifically, we’ll need to add an entry that looks like this:

# tail -1 /etc/fstab

/dev/sdb1               swap              swap    defaults        0 0

Finally, we need to inform the kernel that it has new swap space available.  We’ll use the swapon command for that:

# swapon -av

swapon on /dev/sdb1

swapon: /dev/sdb1: found swap signature: version 1, page-size 4, same byte order

swapon: /dev/sdb1: pagesize=4096, swapsize=1074774016, devsize=1074774016

We can verify our work with free -m and swapon -s:

# free -m

total       used       free     shared    buffers     cached

Mem:          1893       1269        623          8         46        820

-/+ buffers/cache:        402       1490

Swap:         5088          0       5088

# swapon -s

Filename                                Type            Size    Used    Priority

/dev/dm-1                               partition       4161532 0       -1

/dev/sdb1                               partition       1049580 0       -2

Note the additional space and the inclusion of /dev/sdb1 in the outputs.

If we do not have a free device we may supply a file instead.  This process is slightly different in the beginning.  First, we’ll need to create the file.  We can use the dd command for that:

# dd if=/dev/zero of=/swapfile bs=1024 count=1048576

1048576+0 records in

1048576+0 records out

1073741824 bytes (1.1 GB) copied, 23.1888 s, 46.3 MB/s

Here we’ve created an empty 1GB file containing only zeroes.  The math works out thusly:

1048576 (count) blocks of 1024 bytes (bs) each creates a file of 1073741824 bytes in size.  That is 1048576KB/1024MB/1GB.

Since this file will ultimately be used to hold the unencrypted contents of swapped out RAM pages, we will need to supply some basic security controls to it.

# chmod 0600 /swapfile

# ls -l /swapfile

-rw-------. 1 root root 1073741824 Feb 22 11:19 /swapfile

From this point forward, we may follow the steps from the previous example: use mkswap to set up the file for swapping, alter /etc/fstab, run swapon -av to mount the new swap, verify with free -m and swapon -s.

Logical Volume Manager (LVM)

Logical Volume Manager (LVM) provides a method for aggregating physical storage (physical volumes) into large pools called volume groups.  This pool of space can then be divided into smaller logical chunks called logical volumes, and handed out with a much greater degree of freedom than traditional systems allow.

*   Physical Volumes (PVs) can be created from whole disks, partitions, or LUNs provided from external storage devices (ex. iSCSI or Fibre Channel arrays).
*   Volume Groups (VG) consist of one or more physical volumes.  We must assign at least one physical volume to a volume group at the time of creation, and can add more later if needed.
*   Logical Volumes (LV) consist of a portion of the space belonging to a volume group.  It may span many physical volumes, but can only ever belong to a single volume group.
*   File systems can be written to a logical volume using the same tools that would create them on a disk or partition.

This process is covered later in a practical exercise.  In this space, we will provide an overview of the procedure, and a list of associated commands (and their descriptions).

Physical Volume→Volume Group→Logical Volume→File systems

The first step in the process is to create a physical volume.  For that, we must identify an available disk, partition, or LUN.  We would then execute the pvcreate command against the selected device(s).  The resulting PV(s) would then be available for use by a volume group.

The following are common commands that can be used to create, modify, and destroy or inspect physical volumes:

*   pvcreate – create a PV
*   pvdisplay – display detailed information about a PV
*   pvremove – remove (destroy) a PV
*   pvresize – resize PV to reflect size of underlying device
*   pvs – display information about PVs on a system
*   pvscan – scan devices for LVM (PV) data; update cache

Physical Volume→Volume Group→Logical Volume→File systems

A volume group is so named because it is, literally, a group of physical volumes.  Therefore, to create a volume group, we require at least one physical volume.  More may be specified at volume group creation, or added later with the vgextend command.

The following are common commands that can be used to create, modify, and destroy or inspect physical volumes:

*   vgcreate – create a VG
*   vgdisplay – display detailed info about VG(s)
*   vgextend – add PV(s) to VG
*   vgreduce – remove PV(s) from VG (CAUTION!)
*   vgremove – destroy a VG
*   vgs – display information about VGs
*   vgscan – scan devices for LVM (VG) data; update cache

Physical Volume→Volume Group→Logical Volume→File systems

Logical volumes represent a portion of the physical storage managed by a volume group.  This storage can come from any of the physical volumes backing the volume group. 

A simple way of stating this:

*   Logical volumes can span multiple physical volumes
*   Logical volumes may only ever belong to a single volume group

The following are common commands that can be used to create, modify, and destroy or inspect physical volumes:

*   lvcreate – create an LV
*   lvdisplay – display detailed information about an LV
*   lvextend – add physical extents to an LV
*   lvreduce – remove physical extents from an LV
*   lvremove – destroy an LV
*   lvresize – shrink or grow an LV (-r autoresize resident FS)
*   lvs – display information about LVs
*   lvscan – scan devices for LVM (LV) data; update cache

Once a logical volume has been created, a file system can be written to it. 

Let’s explore this process.  On our example server, we’ve created two free partitions: /dev/sdb3 and /dev/sdb4.  Let’s begin by configuring /dev/sdb3 as a physical volume.

# pvcreate /dev/sdb3

Physical volume "/dev/sdb3" successfully created

Next, we’ll create a Volume Group containing this physical volume.

# vgcreate -v ExampleVG /dev/sdb3

Wiping cache of LVM-capable devices

Wiping cache of LVM-capable devices

Adding physical volume '/dev/sdb3' to volume group 'ExampleVG'

Archiving volume group "ExampleVG" metadata (seqno 0).

Writing physical volume data to disk "/dev/sdb3"

Physical volume "/dev/sdb3" successfully written

Creating volume group backup "/etc/lvm/backup/ExampleVG" (seqno 1)

Volume group "ExampleVG" successfully created

With the VG created, we can now create a logical volume.

# lvcreate -n ExampleLV -l 100%FREE ExampleVG

Logical volume "ExampleLV" created.

Above, we directed lvcreate to use 100 percent of free space.  We could have also specified a specific size with different invocations of either the -l or -L options.  Let’s take a moment to review our work.

# vgs

VG        #PV #LV #SN Attr   VSize    VFree

ExampleVG   1   1   0 wz--n- 1020.00m    0

vg_server   1   2   0 wz--n-   39.51g    0

# vgdisplay -v ExampleVG

Using volume group(s) on command line.

--- Volume group ---

VG Name               ExampleVG

System ID

Format                lvm2

Metadata Areas        1

Metadata Sequence No  4

VG Access             read/write

VG Status             resizable

MAX LV                0

Cur LV                1

Open LV               0

Max PV                0

Cur PV                1

Act PV                1

VG Size               1020.00 MiB

PE Size               4.00 MiB

Total PE              255

Alloc PE / Size       255 / 1020.00 MiB

Free  PE / Size       0 / 0

VG UUID               N53yxi-ZHgJ-Sm3Y-UvNp-ZTOZ-R1yB-EXoPQe

--- Logical volume ---

LV Path                /dev/ExampleVG/ExampleLV

LV Name                ExampleLV

VG Name                ExampleVG

LV UUID                0k0kjK-mQ1a-INjv-nAWk-MzjN-vLHR-c2gCnF

LV Write Access        read/write

LV Creation host, time server.example.local, 2017-07-26 10:39:40 -0500

LV Status              available

# open                 0

LV Size                1020.00 MiB

Current LE             255

Segments               1

Allocation             inherit

Read ahead sectors     auto

- currently set to     256

Block device           253:2

--- Physical volumes ---

PV Name               /dev/sdb3

PV UUID               2g5DhS-hDbh-Lc4n-MgaT-H1hK-rOwn-JMWRam

PV Status             allocatable

Total PE / Free PE    255 / 0

We can see in the output above that our logical volume, ExampleLV, has taken all available space on the volume group.  The sole PV backing our volume group has been completely consumed.  We’ll make a note of this, and return to it in a moment.

Ultimately, the purpose of a logical volume is to serve as backing for either swap or a file system.  Let’s format our logical volume with an ext4 file system.

# mkfs.ext4 /dev/ExampleVG/ExampleLV

mke2fs 1.41.12 (17-May-2010)

File system label=

OS type: Linux

Block size=4096 (log=2)

Fragment size=4096 (log=2)

Stride=0 blocks, Stripe width=0 blocks

65280 inodes, 261120 blocks

13056 blocks (5.00%) reserved for the super user

First data block=0

Maximum file system blocks=268435456

8 block groups

32768 blocks per group, 32768 fragments per group

8160 inodes per group

Superblock backups stored on blocks:

32768, 98304, 163840, 229376

Writing inode tables: done

Creating journal (4096 blocks): done

Writing superblocks and file system accounting information: done

Next, we’ll create a mount point and mount our new file system to it.

# mkdir /LVMtest

# mount /dev/ExampleVG/ExampleLV /LVMtest/

# ls /LVMtest/

lost+found

# df

File system           1K-blocks    Used Available Use% Mounted on

/dev/mapper/vg_server-lv_root

36550464 5288300  30889544  15% /

tmpfs                   969304     228    969076   1% /dev/shm

/dev/sda1               487652   39588    422464   9% /boot

/dev/mapper/ExampleVG-ExampleLV

1011672    1284    958164   1% /LVMtest

Note that the device listed as backing this file system is /dev/mapper/ExampleVG-ExampleLV instead of the supplied device of /dev/ExampleVG/ExampleLV.  This is expected behavior in EL6, as device mapper handles mapping block devices onto virtual block devices for LVM2.  Device mapper also plays a role in disk encryption and software RAID.

As a final exercise, we’ll briefly consider actions we can take when our LV-backed file systems  become full.  The simplest solution is to increase the size of the logical volume. 

Logical volumes will take their space from any of the physical volumes belonging to its volume group.  In our case, there is no space currently available.  To remedy this, we will need to add a new physical volume to the volume group.

# pvcreate /dev/sdb4

Physical volume "/dev/sdb4" successfully created

# vgextend ExampleVG /dev/sdb4

Volume group "ExampleVG" successfully extended

# lvextend /dev/ExampleVG/ExampleLV -L +500M

Size of logical volume ExampleVG/ExampleLV changed from 1020.00 MiB (255 extents) to 1.48 GiB (380 extents).

Logical volume ExampleLV successfully resized.

At this point, we would use resize2fs to resize the file system into the newly available space.  We could also have called lvextend with the -r option, which would have handled file system resizing for us automatically.

Disk Encryption

There are several methods available for encrypting the contents of disks and logical volumes on EL6.  The most common of these in EL6 is the dm-crypt module with the Linux Unified Key System, or LUKS.  Though dm-crypt can be invoked without any LUKS features, this is rarely done.  This is because LUKS provides many features, such as salting, key management, and error checking that plain dm-crypt does not.

To encrypt a device using these tools, we would invoke the cryptsetup utility.  With it, we can apply disk encryption in the following ways:

1) Encrypt a device (such as a hard drive, partition, or LUN) directly.

2) Encrypt the physical volumes of an LVM volume group (LVM over LUKS).

3)     Apply encryption to logical volumes (LUKS over LVM).

LUKS on a Device

Let’s walk through the direct application of LUKS encryption to a hard disk.  The steps we implement here will also, in large part, be applicable to later sections dealing LVM encryption.

To begin, we need to identify a target device.  We can list block devices on our system with the lsblk command:

# lsblk

NAME                             MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT

sda                                8:0    0   30G  0 disk

├─sda1                             8:1    0  512M  0 part /boot

└─sda2                             8:2    0 29.5G  0 part

├─vg_elg6-swap (dm-0)          253:0    0    1G  0 lvm  [SWAP]

├─vg_elg6-slash (dm-1)         253:1    0   10G  0 lvm  /

├─vg_elg6-tmp (dm-2)           253:2    0    1G  0 lvm  /tmp

├─vg_elg6-var.log (dm-3)       253:3    0    2G  0 lvm  /var/log

├─vg_elg6-var (dm-4)           253:4    0    3G  0 lvm  /var

├─vg_elg6-home (dm-5)          253:5    0    2G  0 lvm  /home

└─vg_elg6-var.log.audit (dm-6) 253:6    0    1G  0 lvm  /var/log/audit

sdb                                8:16   0   10G  0 disk

Here we’ve identified a device, /dev/sdb, as our target.  We’ll next need to invoke the cryptsetup luksFormat command to create the encryption layer, supplying the target disk and a passphrase:

# cryptsetup luksFormat /dev/sdb

WARNING!

========

This will overwrite data on /dev/sdb irrevocably.

Are you sure? (Type uppercase yes): YES

Enter LUKS passphrase: Passphrase

Verify passphrase: Passphrase

Our next step is to open the LUKS device for reading and writing.  To do this, we will use the cryptsetup luksOpen command, supplying the name of the base device and the passphrase to open it, along with a MAPPING name:

# cryptsetup luksOpen /dev/sdb encDisk

Enter passphrase for /dev/sdb: <Input Passphrase>

From this point forward, all command will use the name of the mapped device (above, “encDisk”), rather than the base disk.  We now need to format the disk with a filesystem.  In this example, we will use ext4.

# mkfs.ext4 /dev/mapper/encDisk

mke2fs 1.41.12 (17-May-2010)

Filesystem label=

OS type: Linux

Block size=4096 (log=2)

Fragment size=4096 (log=2)

Stride=0 blocks, Stripe width=0 blocks

655360 inodes, 2620928 blocks

131046 blocks (5.00%) reserved for the super user

First data block=0

Maximum filesystem blocks=2684354560

80 block groups

32768 blocks per group, 32768 fragments per group

8192 inodes per group

Superblock backups stored on blocks:

32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632

Writing inode tables: done

Creating journal (32768 blocks): done

Writing superblocks and filesystem accounting information: done

This filesystem will be automatically checked every 27 mounts or

180 days, whichever comes first.  Use tune2fs -c or -i to override.

With this done, we may mount the filesystem through ordinary means.

LUKS and LVM

When working with whole disks, or partitions, encryption is applied to the base device as has been demonstrated.

When working with LVM, the encryption may be applied either at the logical volume layer or at the physical volume layer.  These situations are referred to as “LUKS over LVM” or “LVM over LUKS”.

For most purposes, applying encryption to the logical volume is the best answer, or “LUKS over LVM”.  This is because volume groups may (and frequently do) contain multiple physical volumes.  Applying encryption at the PV layer and then incorporating the encrypted volumes into a volume group is problematic; loss of a key on one PV could lead to loss of an entire volume group.

In any case, the encryption process is ultimately the same for logical volumes as for physical devices; we simply need to supply the location of a logical volume in place of a physical disk or partition.

Automating the Mount Process for Encrypted Devices

The standard process for automating mount operations involves entries in the /etc/fstab file.  This is also the case for encrypted disks, but we have additional considerations. 

As we have seen, encrypted devices cannot be accessed until they have been opened and mapped.   Nothing in the /etc/fstab file accommodates this operation directly.  To address this, we turn to another file:  /etc/crypttab. 

The purpose of /etc/crypttab is to contain mapping information for encrypted disks.  In other words, it will automate the work performed by the cryptsetup luksOpen command.  Note that this file is only consulted at boot time. 

The example below defines how an /etc/crypttab entry may be created, and what the corresponding entry in /etc/fstab might contain:

# echo "encDisk /dev/sdb" >> /etc/crypttab

# cat /etc/crypttab

encDisk /dev/sdb none

# mkdir /secret

# tail -1 /etc/fstab

/dev/mapper/encDisk    /secret          ext4    defaults        1 2

# mount /secret

# ls /secret

lost+found

Above, the example commands succeed because the targeted LUKS device was already open and mapped.  If it had been closed, /etc/fstab would not have automatically consulted /etc/crypttab to open the device.  /etc/crypttab is ONLY consulted at boot.

Keys

When encrypted disks are opened, a passphrase must ordinarily be supplied.  In the case that a boot device is encrypted, this prompt will stop the system from booting until manual intervention occurs.  To avoid this, we may create a cryptographic key, assign it to the device, and supply the key location in /etc/crypttab.

It should go without saying that these keys must be protected.  Below, we demonstrate the creation and assignment of a key:

# dd if=/dev/urandom of=/root/keyfile bs=1024 count=4

4+0 records in

4+0 records out

4096 bytes (4.1 kB) copied, 0.00206224 s, 2.0 MB/s

# chmod 0400 /root/keyfile

# cryptsetup luksAddKey /dev/sdb /root/keyfile

Enter any passphrase: Passphrase

# umount /secret

# cryptsetup luksClose encDisk

# cryptsetup luksOpen /dev/sdb encDisk --key-file=/root/keyfile

# mount /secret

# ls /secret

lost+found

With this done, we now need to edit /etc/crypttab, informing it of our new key:

# tail -1 /etc/crypttab

encDisk /dev/sdb /root/keyfile luks

After a reboot, the new encrypted filesystem will automatically be mounted at /secret.

Module 8:
Processes and Services

When an EL6 system boots, the BIOS locates the boot device and begins reading it, the bootloader (GRUB) loads the Linux kernel and mounts the root file system read-only.  The kernel takes the command line arguments passed to it by GRUB and starts init.

init is the first process and is ultimately responsible for the initiation of all further processes, from remounting the root file system as a read-write device, to configuring networking, to providing a bash prompt for you to log in to.  The kernel does not really count as a process, rather it is the process and interrupt handler that sits below all processes.  An interrupt is simply a signal either from hardware or software that requires attention.

Every process is assigned a Process ID (PID), a unique number that the kernel uses to track processes.  As the first process, init will receive PID 1. 

The exact identity of PID 1 has changed over the years.  EL5 and below versions used a traditional *nix style init, known as sysvinit.  This system traces its origins back to 1981 and was standardized in 1983 with AT&T SystemV Unix.  EL6 departs somewhat from this with Upstart, which replaces sysvinit completely, but largely retains backwards compatibility.  EL7 replaces Upstart with systemd, developed in 2010\. While there has been some contention in around the adoption of systemd, it will likely persist as it is now the standard on many flavors including SUSE, Mint, Debian, Arch, and Ubuntu.

ps, pgrep, kill, pkill, killall

Before you can control processes, you must first identify them.  The best and most direct way to find processes running on a system is with ps.  The most common invocation is ps -ef (everything, full listing) – often passed through grep, cut, or awk; and ps -u username. 

Long ago there was a divergence from the UNIX/POSIX standard by the BSD group.  You may see some people use the BSD style switches (most commonly aux or -aux as an equivalent to
-ef).  Get in the habit of using the POSIX standard switches, as the BSD style switches will eventually be deprecated.

Another handy way to find processes is by the use of pgrep.  For instance, if you want to find the PIDs of ssh processes being run by root pgrep -u root ssh.  If you also want to see the command line that invoked it add -l.  To see the newest process other than pgrep currently running pgrep -nl. 

A process can be controlled by sending it a signal.  There are 64 signals defined in EL6, each defined by a number and a short ALL CAPS word.  The important ones from a system administrator's viewpoint are:

*   1  HUP Reread your configuration file and restart.
*   2  INTEnd, gracefully if possible.  Sent by CTL-c. Cannot be ignored.
*   3  QUITEnd now, provide a core dump if possible.  Sent by CTL-\
*   15 TERMEnd, gracefully.  Can be ignored
*   9 KILLEnd now. Cannot be ignored
*   19 STOPPause.  
*   20 STPPause.  Can be ignored.  Sent by CTL-z
*   18 CONTResume. Sent by job control programs discussed in the next section.

Signals can be sent with the kill command.  The most common invocation is kill -9 PID.  Be aware that if 0 is used as the PID, all processes in the current group are killed (including your login).  If -1 is specified, all processes other than init will be killed.

You can also use pkill which follows the format of pgrep, but adds signaling.  For instance, to kill all processes run by a user pkill -9 -u username.  Multiple processes can be killed with killall.  For example:  killall -9 -v processname, or killall -i -u username. 

jobs, bg, fg, disown

Thus far all the processes you have started have been issued from the command line and have run in the foreground while you watched.  This is not always desirable, you may not want to give up your bash prompt for half an hour while logs are compressed and moved.  You can start a command in the background by putting an ampersand at the end of the line:
tar -czvf /lotsostuff/* tarball.tgz &.

You also have some options to control a job after you have started it in the foreground.  You can suspend a job with CTL-z.  This will show the job is stopped and the job number:
[1]+  Stopped    command. 

You can get a list of all stopped and backgrounded jobs with the command jobs.  To bring the job back to the foreground type fg and the job number.  To resume the job in the background, type bg and the job number. 

Note that job manipulation using bg, fg, and jobs is shell specific.  You cannot bg a job in one shell and fg it in another.  If you leave jobs running in the background and your shell ends, the jobs will terminate.  To prevent this from happening you must disown -h job-number them.  Other switches for disown include -a (all), and -r (only running jobs)

nice, renice, ionice, taskset

There are several different ways to limit and prioritize resource usage, the simplest is based on cpu priority.  Every process has a cpu scheduling priority, known as a niceness value.  This can be found by invoking the advanced formatting options of ps, e.g.:

ps -eo nice,pid,user,comm  << no spaces! 

The niceness value is an integer from -20 to 19, with lower numbers being higher in priority (less nice).  A process started from the command line has a default niceness of 0.  To start a command with a different value, use nice.  Issuing nice command, causes command to start with a niceness of 10.  You can either use nice -n value to set a different value or simply nice -value.  Be aware that to set a negative value without using -n you must use two dashes:
nice --19 command.  If issued with one dash nice sets a positive 19 value.

Once a command is running its niceness can be adjusted using renice.  This can even be done for all processes owned by a user thus: renice -10 -u username.

Processes can also have a scheduling priority for disk access.  This can be viewed and controlled using ionice, which allows scheduling in classes of realtime, best-effort, or idle time only.

A given process can be assigned to run on a specified processor or processor set.  This is known as processor affinity and while not often done, it can have performance benefits.  In EL6 processor affinity is set using taskset.

limits.conf, ulimit

You can place limits on the resource usage of a given user or group using the file /etc/security/limits.conf.  It takes these columns:

*   domain – a user, a group (preceded by @), or * for default
*   type – hard, never to be exceeded; or soft, adjustable by the user up to a hard limit
*   item – what we are limiting, options include:

    *   fsize – maximum filesize (KB)
    *   memlock – max locked-in-memory address space (KB)
    *   nofile – max number of open files
    *   cpu    – max CPU time (MIN)
    *   nproc – max number of processes
    *   as     – address space limit (KB)
    *   locks – max number of file locks the user can hold
    *   nice – max nice priority allowed to raise to values: [-20, 19]
    *   priority – process priority default
    *   maxlogins – max number of logins for this user
    *   maxsyslogins – max number of logins on the system
*   value

Limits can be adjusted on the fly using the bash built-in ulimit.  If you impose default limits using limits.conf, it is recommended that ulimit -u unlimited be added to root's bashrc.  This will keep root from being restricted.

Note: ulimit -a does not report limits correctly in EL6.

top, uptime, free, vmstat

You can view and control running processes using the top command. This displays a header bar summarizing the state of the system:

top - 08:36:00 up 17:53,  2 users,  load average: 3.21, 0.76, 0.31
The first line displays the current time, uptime since last boot, number of logged in users, and load average – the number of processes waiting in the cpu queue over the last 1, 5, and 15 minutes.  This line is also displayed in the output of w and uptime.

Tasks: 163 total,  12 running, 150 sleeping,   1 stopped,   0 zombie
The Tasks line shows the number of processes: total, running, sleeping (waiting for something to happen), stopped (via CTL-Z or a STOP signal), and zombies (those that have terminated, but not fully exited).

%Cpu(s):100.0 us, 0.0 sy, 0.0 ni, 0.0 id,0.0 wa,0.0 hi,0.0 si, 0.0 st
The Cpu display can be switched between cumulative and per cpu statistics by pressing 1. The numbers on the %Cpu line are:

*   user – all programs that don't belong to the kernel
*   system – kernel programs, such as networking or I/O operations
*   nice – time spent running programs that have been niced
*   idle – time spent doing nothing
*   wait – time spent waiting for the outside world such as I/O
*   hi & si – time spent servicing hard and soft interrupts
*   stolen – only seen on virtual machines hosted on Linux.  This is the time spent waiting for cpu because another VM was using it.

KiB Mem:2916168 total, 2053344 free,  384916 used,  477908 buff/cache
KiB Swap:  3776504 total,  3776504 free,    0 used.  2290980 avail Mem
The Memory and Swap lines should be self-explanatory, with the exception of buff/cache – which is the amount of memory used by the kernel in pre-read buffers and write caches.  This information can also be obtained in a more readable format with free -h; and in a less readable format, but with more detail using vmstat.

Below the header is a list of processes:

PID USER  PR  NI    VIRT    RES   SHR  S  %CPU  %MEM  TIME+   COMMAND

649 root  20   0  228920   6228   4632 S   0.3  0.2   0:41.06 vmtoolsd

*   PID, USER – the PID, and user who issued the command.
*   PR & NI – The scheduling priority and niceness value.
*   VIRT – Virtual image: the total memory size of the process, including all shared libraries, pages swapped out to disk, and pages allocated, but not used.
*   RES – Resident memory: the actual physical memory in use.
*   SHR – Shared memory: or at least potentially shared memory (such as libraries).
*   S – Status:

    *   Running
    *   Sleeping
    *   sTopped
    *   Zombie
    *   Dead (uninterruptible sleep)
*   %CPU, %MEM, TIME+ – Percentages of cpu and memory, as well as total cpu time taken.  Note that %CPU is based on one core and may exceed 100% in a multicore system.
*   COMMAND – the command name.

There are a number of commands that can be issued within top.  Here are a few cool ones:

*   h – Display a help screen
*   d – set update interval in seconds
*   i – toggle idle processes
*   n – Change the number of processes displayed.
*   f – Select fields to display
*   F – Select sort field
*   M – Sort by memory usage.
*   P – Sort by CPU usage.
*   T – Sort by cpu time.
*   R – Reverse sort order
*   <> – Move through sort fields
*   V – Show parent process relationships
*   c – show full command line
*   u – Filter by user.
*   r – Renice a process.
*   k – Kill a process.
*   W – Save current configuration to ~/.toprc
*   q – quit top

cgroups

While beyond the scope of this course, there is another method of controlling access to resources.  Introduced in EL6, control groups (called cgroups) are a powerful tool which can effectively divide a machine into pools of resources and restrict a process tree to that pool.  By default cgroups are not fully implemented or user controllable in EL6.  In EL7, they are an integral part of the process structure as systemd runs everything in cgroups.  If you wish to explore further, [https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Resource_Management_Guide/ch01.html](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Resource_Management_Guide/ch01.html)

Module 9:
Scheduling Events

at, atq, atrm, batch, atd, at.allow/.deny

It's often useful to be able to schedule tasks in the future, either once or recurring on a regular basis.  The simplest way is to use the command at.  To create a future job, type at followed by a time. Then press enter, you will then have an at> prompt to input commands.  When done exit with CTL-d.  You will see the job has been scheduled. It is pretty liberal regarding the format of time.  All the following are acceptable: 

*   midnight
*   now + 1 hour
*   4pm
*   16:00 Aug 10 2018
*   noon tomorrow

You can view scheduled jobs using atq, and remove them by number using atrm.  To see the full command set to be run, find the job number using atq, then at -c X.

If you wish to run a computing intensive job when there is less load on the system, you can use batch, which is a special invocation of at.  It is used just like at only without a time parameter.  Jobs queued using batch only run when cpu utilization is below a certain limit.  This limit is adjusted using at -l, and has a default of 0.8.  This was a reasonable number when the program was written over two decades ago.  Most recommendations today suggest that it be set higher, around or above the number of available cores minus 1.  If you wish to set the limit to essentially only idle time: at -l 0.01.

It is worth noting that at runs jobs sequentially, and will not start the next until the first has completed.  Whereas batch can overlap jobs, starting them with a default 60 second offset.

If you wish to limit who can schedule jobs using at and batch, you have two choices.  Create a file called /etc/at.allow and place only the users you wish to allow into the file – one name per line, no whitespace. This is the preferred method  Alternatively, you can put those you wish to deny into /etc/at.deny.

crond, cronie

While at and batch allow you to schedule a job in the future, they only provide the ability to schedule a task once.  To schedule a recurring job, you must use the crond service, which provides the cron feature and its extension anacron.  These are provided by two software packages: cronie and cronie-anacron.  Before using cron, check that it is installed and running with # service crond status.

cron and anacron provide similar, but not identical, functionality. 

*   cron:

    *   exact time specified
    *   granularity of one minute
    *   available to normal users by default
    *   will also run any file in /etc/cron.hourly by default
    *   can run jobs simultaneously
    *   will not run a job if the time to run is missed
*   anacron:

    *   called hourly from cron (using /etc/cron.hourly/0anacron)
    *   includes start time randomization
    *   smallest possible interval is one day
    *   restricted to root
    *   will start a missed job when possible
    *   runs jobs sequentially
    *   will run all executable files in /etc/cron.[daily, weekly, monthly]

anacron, run-parts, /etc/anacrontab

The usual way to use anacron is to write a script – often just a one or two liner with the command you wish to run, put it in /etc/cron.interval, and chmod it to be executable.  It will then be run (niced) at the appropriate interval using the /usr/bin/run-parts script, if you wish to modify the behavior of run-parts, it has a configuration file at /etc/sysconfig/run-parts.  If you wish to prevent an anacron job from running, create a file called jobs.deny in the appropriate directory and specify in it the name of the file you want to disallow.

You can also add a line directly into /etc/anacrontab using the following format

3    21    bob.job  /home/bob/custom.script

This would run custom.script as a job called bob.job every 3 days.  The time it will run is 21 minutes after the beginning of the START_HOURS_RANGE, plus a random amount which has a maximum of RANDOM_DELAY.  These values can be adjusted in anacrontab.

cron, crontab

There is a configuration file /etc/crontab.  It should only be altered if you wish to change the global behavior of cron by changing the variables in it such as PATH.  You may encounter documentation saying that you should schedule jobs by editing this file. It should never be used for this purpose.  Some documentation also says that you should specify the user who will run each job.  This is also wrong. 

Instead, to manipulate cron, use crontab.  This will create a separate file for each user.  If you have used su to change your effective UID, use the switch -u username to specify the user as crontab can be "confused" by effective UIDs.  To edit the a crontab, use crontab -e; which will create a file in /var/spool/cron. Then add a line of the following format:

15   11   2-31/2   *   mon-fri   /usr/bin/wall "Rus buys lunch!!"

In this example the first five fields specify the times that this command will run.  They are:

*   minutes – 15 minutes after the hour (allowable range is 0-59)
*   hours – 11am (0-23)
*   day – the 2nd day of the month to the 31st day of the month, in intervals of two (1-31)
*   month – any month (1-12 or jan-dec)
*   day of week – Monday through Friday, inclusive.  This could have also been specified as 1-5 (0-7 or sun-sat; where 0 and 7 both represent Sunday)

All time fields must match for the command to run.  So, this command will run at 11:15 am on even numbered weekdays.  The * is used to specify a value of any.  Values can also be entered separated by commas (no spaces).  For a job to run at 1 am on the first day of every quarter:

    0    1    1    1,4,7,10    *      /path/jobname

Be careful with your *; if there had been one where the 0 is in the above line, the job would try to run every minute from 1:00 to 1:59.  Unlike on older systems, in EL6 there is no need to restart crond after edits, it will pick up the changes at the next minute.

All users can use cron by default.  On a secure system this is not desirable.  Like the at command, you can create either /etc/cron.allow or /etc/cron.deny to control access.  You can also control access via PAM (Pluggable Authentication Modules) by adding the line
-:ALL EXCEPT root :cron  to /etc/security/access.conf.

Module 10:
Booting

The boot sequence of a EL6 system is:

*   BIOS / UEFI – firmware which checks the hardware, initializes it, and specifies (or in the case of UEFI without compatibility support detects) the boot device.  Most current implementations of UEFI run with the compatibility support module (CSM) enabled. 
    It will then load the bootstrap program from the either the MBR (BIOS or CSM) or a separate /boot partition (UEFI).

*   Bootstrap

    *   MBR – the first 512 bytes on the boot device; containing boot.img in the first 446 bytes, followed by four 16-byte Primary partition tables, and a two-byte magic number (xAA55).

        *   boot.img in turn loads core.img
        *   core.img is written in the empty space left between the MBR and the beginning of the first partition.  It loads configuration files, and other modules needed to boot, such as file system drivers.  core.img is generated during installation.
    *   UEFI – will read from a special boot partition (either /boot/efi or /efi/BOOT).  The file will typically be named something like grubx64.efi. 

        *   The integrity of grubx64.efi and of the kernel are validated using keys stored in a file called shim.efi.
    *   Either of these will then start the grub process.
    *   Additional or alternative images may also be loaded, for instance to PXE boot.

*   grub – is the bootloader for RHEL Linux.  It will read a grub.conf and provide a text menu based on it to select an operating system.  Typically grub will then:

    *   Mount the file system in read-only mode
    *   Load the kernel from a compressed file (vmlinuz)
    *   Mount an initial read-write file system in RAM (initrd16) and load an image into it which will have the remainder of the necessary modules and instructions to load the actual run-time kernel for use.  The image contents can be viewed using lsinitrd.
    *   Mount the root file system in read-write mode, then start the kernel.  At this point logging to the kernel ring buffer begins.  These logs are viewable with dmesg.
    *   Much of this is done through a program called dracut.  Any options you see that start with rd. are options passed to dracut.
    *   The kernel will then launch init

*   init – in EL6 init is really called upstart, but it is never invoked as such.  It is the first userspace process which initiates all other processes.  It will

    *   determine the targeted runlevel as specified in /etc/inittab
    *   mount file systems listed in /etc/fstab
    *   run /etc/rc.d/rc.sysinit and the appropriate scripts in /etc/init
    *   execute the scripts in /etc/rc.d/rclevel.d. 
    *   run the script /etc/rc.local.  This is run at boot, and at runlevel change.

        There is some confusion in the official documentation regarding scripts in /etc/event.d.  This was an upstart feature that was never fully implemented in EL6 and which is totally superseded in EL7. 

Enabling services

Services (also known as daemons) can be turned on with # service servicename start.  The service command runs the appropriate script located in /etc/init.d with an argument of the command supplied (in this case start).  Other useful commands that go with service include stop, restart, and force-reload.  If issued as # service --status-all, it will return the status of all services. 

When an EL6 system boots, the first program run by the kernel is /sbin/init, which will examine the configuration file /etc/inittab to determine the target runlevel.  The relevant line in inittab looks like this:

id:3:initdefault:  Where 3 is the default run level.

EL6 has six runlevels:

*   0 – halt, stop all processes (Do NOT set initdefault to this)
*   1 – Single-user mode, for maintenance and disaster recovery
*   2 – Multi-user, without NFS
*   3 – Multi-user mode, normal text only mode for servers
*   4 – unused
*   5 – X11, full graphical mode.
*   6 – reboot (Do NOT set initdefault to this)

Under normal circumstances you will work under either runlevel 3 or 5.  The previous and current runlevel can be viewed by issuing the command runlevel.  This will return two numbers, the previous runlevel and the current.  If there was no previous runlevel, the first character will be an N.

Changing from one runlevel to another is accomplished by issuing telinit X. Where X is the desired runlevel.

The services which will run at a given runlevel are defined in a numbered directory /etc/rc.d/rcX.d, where X is the runlevel.  Files should not be put directly into these directories, instead links should be created to the actual scripts which are stored in /etc/init.d.  The links begin either with a K (services that should be killed), or an S (services that should be started).  They are processed in numeric order.  If two scripts have the same number, they will be processed alphabetically.

You can manually create these links, but it is not recommended. Instead use chkconfig, which will automatically create them: # chkconfig sshd on.  You can see which levels sshd will run in with # chkconfig sshd --list.  If you wished to turn sshd off for runlevel 2 and 4 this can be done thus: # chkconfig sshd --level 24 off.  Alternatively, a simple menu driven interface can be invoked using # ntsysv --level runlevel. 

A full list of services and their associated runlevels can be obtained by simply issuing chkconfig with no arguments. 

grub, grub.conf,

On boot grub will read /etc/grub.conf to determine what menu it should present and how it should boot.  This file is a link to either /boot/grub/grub.conf or /efi/boot/grub.conf, depending on the system architecture.  For security, ensure that this file is owned by root:root with permissions of 600.

Things you might change in /etc/grub.conf are:

*   default – the index number of the default menu entry (counts from 0)
*   timeout – number of seconds before executing the default

    *   If set to 0 there will be no grub menu.  This can be overridden by pressing shift.
*   hiddenmenu – hides the menu during the timeout

*   Remove kernel arguments:

    *   rhgb – prevent Red Hat Graphical Boot, which hides boot messages
    *   quiet – do not hide boot messages
    *   confirm – this allows booting interactively which means a user could disable crucial services, such as firewall or SELinux.

        *   To further prevent this the PROMPT=no directive in /etc/sysconfig/init should be set.

*   Add kernel arguments:

    *   audit=1 –audit processes that start before the audit daemon, required.
    *   selinux=1 – ensure SELinux is on, this is required.
    *   enforcing=1 – ensure that SELinux is enforcing, also required.

        *   enforcing=0 – set SELinux into permissive mode, it will log violations, but not prevent them. Occasionally used for troubleshooting/recovery.  This must not be a default configuration!

The boot process can be changed during boot as well.  This is done by pressing any key during the timeout period, then a to append to the kernel arguments line.  In addition to the arguments listed above you can also pass the runlevel to be targeted at boot (1, 3, 5). You can see which kernel arguments were passed during the current boot with cat /proc/cmdline or with the dmesg command.

Another way to alter grub configuration is with the use of grubby, though it is often more trouble than it's worth.

To prevent unauthorized alteration of the boot sequence you should set a password on grub itself.  To do this:

*   vi /etc/grub.conf
*   insert a new line, after splashimage, but before the first title
*   place the cursor there, escape to normal mode
*   :r !grub-crypt --sha-512 , this will generate a password hash

    *   enter a new password twice
*   insert password --encrypted before the password hash, on the same line.

Note that the grub password for should not be the same as root's login password.  Some documentation will still mention the use of grub-md5-crypt.  This should not be used at any time as md5 is no longer considered secure.  You should also comment out or delete any unneeded menu entries. 

recovering root password

If you have lost the root password you can recover it by using single user mode (runlevel 1):

*   Interrupt the boot sequence, press a to alter the kernel command line

    *   set selinux=0
    *   append 1 to the end of the line, to invoke single user mode
*   reset the password for root
*   Because you made changes to the file system when SELinux wasn't looking it's best to make sure that the security contexts are correct:

    *   If you only reset a password, restorecon /etc/shadow.
    *   If you know that you altered other files, you can run restorecon against them as well.
    *   If you aren't sure, touch /.autorelabel.  This will fix security context on all files in the file system.  It takes longer, but it's safer.
*   reboot

Some documentation says that the steps above involving SELinux are not required.  This varies between implementations of EL6.  If you aren't sure, it is best to be safe as you could actually brick the system otherwise.

reboot, halt, poweroff

You can control the power state of an EL6 box by simply using telinit and the appropriate runlevel.  Zero will poweroff, one will halt, and six will reboot.  These are also commands themselves which do nothing but invoke telinit.  If these commands are passed with -f, the normal shutdown procedure is skipped and the runlevel is switched immediately. 

Alternatively you can use the shutdown command.  In its most common invocation this is:  shutdown -r now, where -r reboots.  To power off a system shutdown -P.

Module 11:
Logs

dmesg, logger introduction

When a Linux machine boots it immediately begins logging kernel messages to the kernel ring buffer, a 16 KB first-in/first-out over-writable block of memory.  These messages will be passed to the system logger service when it becomes available.  In EL6, the traditional syslog service has been replaced by rsyslogd, which is compatible with older systems.  It will take configuration files in the older syslogd format and stores messages traditional plain text log files. 

If for some reason rsyslogd does not start, boot messages can still be read using dmesg.  Here you can see the command line switches passed to the kernel by grub, the device driver messages, init beginning, etc.

rsyslogd, rsyslog.conf, remote logging, RELP, logrotate

rsyslogd is nothing but a message router with dynamically configurable inputs and outputs.  It can take inputs from /dev/log/ and/or a network socket.  It then parses, filters, and formats the inputs.  It can output the messages to a file, a database, or a remote system.  It supports digital signature and encryption of messages sent to a remote system. 

The main configuration file for rsyslogd is /etc/rsyslog.conf.  The first portion of this file is devoted to the loading of modules, which provide all inputs and outputs to rsyslogd and are activated by the $ModLoad directive.  The modules here allow everything from the reading of kernel messages to direct interaction with an SQL database. 

Below the Modules section are the Global Directives.  These options control the overall behavior of the rsyslogd daemon.

The final portion of rsyslog.conf contains the Rules for handling messages.  Each line will have a message classification and destination.  The message classification has two parts:  the facility (the origin of the message), and the severity.  Asterisks are used as wildcards.  Relevant facilities and severities are:

*   Facilities:

    *   kern – kernel messages
    *   user – user-level messages
    *   mail – mail system
    *   daemon – system daemons
    *   authpriv – security/authorization messages
    *   cron – scheduling daemon
    *   local7 – local use 7 (boot messages)
*   Severities (aka priority):

    *   0emerg – System is unusable.
    *   1alert – Action must be taken immediately.
    *   2crit – Critical conditions, such as hard device errors.
    *   3err – Error conditions.
    *   4warning – Warning conditions.
    *   5notice – Normal but significant conditions.
    *   6info – Informational messages.
    *   7debug – Debug-level messages.
    *   .none – Do not log

Destinations can be:

*   A file

    *   Standard logs include /var/log/…messages, secure, cron, maillog, boot.log
*   STDOUT such as /dev/console
*   A remote machine. 

    *   UDP is specified with a single @hostname:port
    *   TCP is specified with a double @@hostname:port
*   An output module:

    *   :omusrmsg:* – message everyone using wall
    *   :omrelp: – use the Reliable Event Logging Protocol
*   A filter – if you have advanced needs
*   Discard – specified with a ~. Any messages discarded will not be processed in a lower rule:  *.* ~ ends all processing.

The STIG requires that logs be sent to a remote server.  The recommended way to do this however does not take into account the inherent unreliability of the standard syslog transfer method.  If the remote server is not available or the local machine crashes, messages will be lost. Rather than issuing *.* @@servername:514 in rsyslog.conf as specified in the STIG, you should use RELP if available. 

Note that the specification *.* will log everything, you may want to reduce this by specifying *.info, which will record everything at the info level and above.

If RLEP is not available, uncomment the lower block of the example forwarding rule and configure it appropriately for your environment.  This creates an on-disk queue which will be retransmitted if need be.

To configure RELP, in rsyslog.conf:

*   Aggregator:

    *   $ModLoad imrelp
    *   $InputRELPServerRun 2514
*   Sender

    *   $Modload omrelp
    *   *.* :omreplp:10.1.1.250:2514
*   On Both:  semanage port -a -t syslogd_port_t -p tcp 2514

The STIG also specifies that unless this machine is an aggregation server and documented as such, it should not receive logs from other machines.  This is done by ensuring that the modules imudp, imtcp, and imrelp are not loaded.  The STIG only mentions imtcp.

Retention and rotation of rsyslogd files is accomplished by logrotate, which is called by cron.daily.  It is configured in /etc/logrotate.conf and associated files in /etc/logrotate.d.

You can generate your own messages that will be sent to the logging services using the utility logger, which allows you to specify priority with -p.  For instance, this:
# logger -p cron.warning test would place a message test in the log as a warning from cron.

setting the timezone, date, hwclock ntp – Setting the time

Maintaining accurate time on computers is essential for certificate based encryption and authentication as well as for logging.  Log entries are only as good as the time stamp associated with them. 

The file /etc/localtime contains the timezone information for your machine.  To configure the timezone, we will create a symbolic link from /etc/localtime to a pre-built configuration file.  To do this:

*   Display current timezone using date.
*   Determine which file you will link to:

    *   Use the tzselect command and follow the menus
        OR
    *   Search /usr/share/zoneinfo using ls.
    *   ln -s /usr/share/zoneinfo/America/Chicago /etc/localtime
*   Confirm that it worked:

    *   Verify the timezone using date.
    *   You can also view the contents of /etc/sysconfig/clock using less.

Now we can set the time and date using the date command:
date -s "24 july 2017 16:21:00"

The last step of the manual time-setting process is writing the system (software based) time to the hardware (BIOS) clock.  This is accomplished with hwclock -w. 

To ensure accurate time in EL6 we rely on ntpd.  The configuration of ntp is straightforward:

*   Check that the timezone and current time are correct.  A few minutes accuracy is close enough.  If the time is incorrect, date -s HH:MM:SS
*   Perform a manual sync: ntpdate servername.
*   Edit /etc/ntp.conf.  Configure the upstream ntp server(s):

    *   Usually your network will have an ntp server; if so use it. 
    *   If not, some alternatives are:

        *   time.nist.gov
        *   tick, tock & ntp2.usno.navy.mil for east and central
        *   tick & tock.usnogps.navy.mil for mountain and pacific. 
        *   x.us.pool.ntp.org or
            x.rhel.pool.ntp.org, the defaults for the civilian world
    *   Remove any burst or iburst directives.  These were primarily designed to account for call setup time in modem based or ISDN networks and will send bursts of packets to unreachable servers.  This is an unwanted behavior on a modern network.
*   Start and enable ntpd with service and chkconfig
*   Verify using ntpq -p

If this machine is to be a server as well:

*   define the network you wish to allow access:
    restrict 192.168.0.0 mask 255.255.0.0 kod nomodify notrap nopeer noquery

    *   mask – if none is specified, /32 is presumed
    *   kod – send a kiss of death packet to quelch over-active clients
    *   nomodify – ignore attempts to change configuration
    *   notrap – ignore control message traps
    *   nopeer – do not form a peer association
    *   noquery – ignore anything other than a time query
*   open the appropriate port
    iptables -I INPUT 5 -p udp -m state --state NEW -m udp --dport 123 -j ACCEPT

Module 12:
SELinux

SELinux is a security module for the Linux kernel, and provides a means of implementing Mandatory Access Controls in a secure system.  The term access control is taken to mean a method for preventing the use of a resource by an unauthorized party or in an unauthorized manner.

In Discretionary Access Control (DAC) models, users are given control over the resources that they own.  Standard Linux permissions represent a type of discretionary access control.  While this model can prevent unauthorized users and processes from reading, writing, or executing disallowed files, it does not provide any methods for preventing a user or process from performing undesirable actions against resources they would otherwise be permitted to control. 

For example, DAC cannot prevent a user from giving other users access or even ownership over files they own.  Similarly, DAC cannot prevent processes a user spawns from accessing or modifying files accessible to the invoking user.  In the case that a process running with root privileges were to be hijacked by a malicious actor, the entire system could be at risk.

Mandatory Access Control (MAC) models provide a way to resolve these issues.  The SELinux implementation of MAC accomplishes this by labelling and classifying the resources and participants on a system, and specifying rules for if and how they may interact.  These rules cannot be violated by any user or process.  Certain system operators may change policies or place SELinux into permissive mode, but they are still subject to the SELinux enforcement rules that they create.

NOTE: SELinux does not replace DAC permissions; it is layered above them.  It cannot, for example, grant permissions that DAC permissions have denied.  DAC is always consulted first.  SELinux may, or may not, apply additional controls.  The order of operations is:

*   System Call – a command is issued.
*   Error Check – is it a valid command?
*   DAC (Permissions / ACLs) – is the user allowed to read, write, execute as needed?
*   MAC (SELinux) – is this allowed under the security context?
*   Return – execute command, or exit with error (possibly logging)

SELINUX in 5 Minutes

SELinux provides a MAC model, laid on top of the default DAC of traditional Linux.  The central mechanism of SELinux is called “Type Enforcement”.  Type Enforcement controls interactions between different types of system resources.  Every resource in SELinux will be assigned a type.  These resources could be processes (which are often referred to as Subjects) or files, directories, ports, etc. (often called Objects, or “those things that the Subjects interact with and manipulate”).

Before we go further, we should cover some basic terminology that will help us understand how SELinux protects a system:

*   OBJECT – a system resource; the target of interaction by SUBJECTS.  These can be files, devices, ports – practically any sort of system resource.
*   SUBJECT – an active component, something that attempts to interact with OBJECTS and other SUBJECTS.  Simply put, these are processes.
*   TYPE – a way of categorizing resources on a system.  When we assign a type to a process, we would say that we have assigned that process to a DOMAIN.  When we assign types to OBJECTS, we simply retain the designation of “type”.
*   DOMAIN – a context in which processes are executed.  Policy rules are applied to these.
*   POLICY – the driver for SELinux enforcement.  Policy modules can be created which contain rules and definitions for types and domains (and more).  These rules can take a variety of forms, from granting or revoking access and privileges to controlling transitions between domains, to controlling object type transitions inside a domain, to controlling auditing behavior, etc.   
*   SECURITY CONTEXT – made up of an SELinux User, a role, a type, and a sensitivity/classification level in a colon delimited label.  Here is a label setting user=system_u, role=object_r, type=var_t, and sensitivity=s0:   
    system_u:object_r:var_t:s0.

    *   SELinux User – a class of user, such as sysadm_u, staff_u, or system_u.  These aren’t classic Linux users.  Rather, classic Linux users (and every other resource on the system) would be assigned to one of these classes.  If Role Based Access Control (RBAC) is not being implemented, these aren’t typically an object of consideration; instead, processes run under system_u, and users receive unconfined_u. 

Below, we see system logins and their assigned SELinux user class.  If semanage is not available on your system, install policycoreutils-python:

# semanage login -l

Login Name           SELinux User         MLS/MCS Range       

__default__          unconfined_u         s0-s0:c0.c1023      

root                 unconfined_u         s0-s0:c0.c1023      

system_u             system_u             s0-s0:c0.c1023      

*   Type – As stated earlier, a way of categorizing resources.  The /var/ftp directory, for example, has a default type of public_content_t while the syslog daemon, rsyslogd, has a type (domain) of syslogd_t.  This is because the /var/ftp directory frequently hosts publicly accessible content, and rsyslogd is responsible for logging system events. 

Remember, when types are assigned to processes, we call them domains; when we assign them to objects, they are (annoyingly) simply called types. 

*   Roles – Roles determine which domains a user class can access.  A brief description of the relationships between roles, users, and domains:

    *   System Resources are assigned to an SELinux User class;
    *   User classes have access to Roles;
    *   Roles have access to Domains;
    *   Domains have access and permissions to Objects or other Domains as defined by policy rules. 

When RBAC is not implemented, roles are not a consideration; instead, both system_u and unconfined_u will be assigned the system_r and unconfined_r roles.  Objects will be assigned the somewhat arbitrary object_r role, which functions mainly as a placeholder in preserving the syntactic integrity of the security contexts.

See below for details (trimmed):

# semanage user -l

SELinux User – SELinux Roles

system_u – system_r unconfined_r

unconfined_u – system_r unconfined_r

The effect of this is to make users and roles essentially meaningless, while still enforcing against them in the kernel (in case RBAC is implemented later).

*   Sensitivity – Sensitivity is a component of the Multi-Level Security and Multi-Class Security enforcement methods.  Sensitivity descriptors were developed for highly secure, compartmentalized environments.  There are 16 sensitivity levels (s0-s15) and 1024 classification levels (c0-c1023).  A full treatment of MLS/MCS is beyond the scope of this material.  Interested parties should begin with the NSA’s publications on SELinux or (for the especially adventurous) any papers dealing with the Bell-LaPadula security model.

Labels

Labels are a representation of the security context assigned to a resource. In many commands, there is a standard option, -Z, which will cause these labels to be displayed alongside other output. 

Let’s examine a few of these labels.  The most important component in these labels, from our perspective, is the type.

# ls -Z /var

drwxr-xr-x. root root system_u:object_r:var_t:s0       adm

drwxr-xr-x. root root system_u:object_r:public_content_t:s0 ftp

# ps -efZ

LABEL – – CMD

system_u:system_r:init_t:s0 /sbin/init

system_u:system_r:kernel_t:s0 [kthreadd]

system_u:system_r:auditd_t:s0 auditd

system_u:system_r:rpcd_t:s0 rpc.statd

# id -Z

unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023

Types and Domains

To briefly recap, we have learned that types provide a way to classify resources on a system, and that Type Enforcement is used to control how these resources may interact. More specifically, we have learned that processes (or Subjects) are typed into domains.  There are three types of Domains: confined, unconfined, and permissive.

Confined Domains are domains where typical SELinux enforcement controls are operating.  Policies and rules define how these domains may interact with other domains, or with other resources on the system. 

Unconfined Domains, in theory, function as if there were no SELinux controls against them.  In other words, processes running in these domains default to DAC for security.  This is not expressly true in that controls CAN be applied to these domains.  Rather, it is more correct to say that they typically are not.  Examples of unconfined domains include unconfined_t and unconfined_service_t.  We can get a list of unconfined domains on our system by using the seinfo command which is part of the setools-console package. 

The list below is trimmed to include some of the more interesting unconfined domains:

seinfo -aunconfined_domain_type -x #no space after -a

unconfined_domain_type

kernel_t

crond_t

init_t

initrc_t

lvm_t

mount_t

unconfined_service_t

unconfined_t

Permissive Domains make up the third domain type.  These domains have all of the framework in place to be considered confined domains, but enforcement has been selectively disabled for them.  Permissive domains will still generate SELinux audit logs for exceptions that would have been blocked, but do not block processes from performing actions that would otherwise have been disallowed.  These are not commonly implemented on mature processes.  Rather, they exist mainly for testing purposes.

We can retrieve a list of permissive domains with the semanage command:

# semanage permissive -l

Customized Permissive Types

Builtin Permissive Types

sanlk_resetd_t

hsqldb_t

systemd_hwdb_t

blkmapd_t

ipmievd_t

targetd_t

An example scenario

We can gain a better understanding of how these domains function by exploring a typical scenario.  On our example server, we have installed an Apache web server.  In this scenario, management has requested three things of us:

1.  Allow users to share the contents of their home directories via http
2.  Change the document root from /var/www/html to a new directory - /web
3.  Change the port that httpd listens on to 8000.

A quick alteration of the /etc/http/conf/httpd.conf file configures the server to accept these changes.

Task 1

We start by enabling users to share their home directories.  We check our work and ensure that everything is correct. 

However, when we attempt to access a user’s home directory, our web browser reports an error:

403 Forbidden

You don’t have permission to access XXXX on this server.

We can determine if this is an SELinux conflict in a couple of ways.  This first and most obvious is to place SELinux into Permissive mode and see if the problems are resolved.  We can do this using the setenforce command:

# setenforce 0

# getenforce

Permissive

With SELinux set to “Permissive”, exceptions will be logged, but not enforced.  If a previously failing action is successful in Permissive mode, we can reliably assume that SELinux was causing the denial.

We can also check logs to see if any exceptions have been noted.  Since this error would have occurred fairly recently, we can use tail to retrieve the last few lines of /var/log/messages, and pipe that through grep to filter for AVC (access vector cache, related to SELinux permissions).

# tail /var/log/messages | grep httpd

Jul 25 10:37:02 server setroubleshoot: SELinux is preventing /usr/sbin/httpd from read access on the file index.html. For complete SELinux messages. run  sealert -l 5438c260-c106-42d1-8cd8-7e2510ac78ce

This output does indicate an SELinux action against httpd, but it’s not terribly informative.  We can get a better look at the errors by following the advice highlighted in the message

NOTE: If your system does not have the sealert command, or if no SELinux messages are being written to /var/log/messages, you will need to install setroubleshoot-server:

# sealert -l 5438c260-c106-42d1-8cd8-7e2510ac78ce

SELinux is preventing /usr/sbin/httpd from read access on the file index.html.

*******  Plugin catchall_boolean (47.5 confidence) suggests  *********

If you want to allow httpd to read user content

Then you must tell SELinux about this by enabling the 'httpd_read_user_content'boolean.

Do

setsebool -P httpd_read_user_content 1

Here we can see that SELinux is preventing httpd from providing read access to the user’s home directory.  We can also see a helpful suggestion: check the SELinux Booleans.

SELinux Booleans are like security toggle switches.  These are common policy changes that operators might want to enable, and are provided to us so that we will not be required to create and apply policy modules (which may result in a more degraded security posture than we would like).

We can get a list of SELinux Booleans with the getsebool command (or a similar list with semanage boolean -l).  Since we only wish to see booleans relating to httpd, we will again filter the results with grep:

# getsebool -a | grep httpd

allow_httpd_anon_write --> off

allow_httpd_mod_auth_ntlm_winbind --> off

<truncated>

httpd_enable_ftp_server --> off

httpd_enable_homedirs --> off

httpd_execmem --> off

httpd_manage_ipa --> off

httpd_read_user_content --> off

httpd_run_preupgrade --> off

httpd_run_stickshift --> off

httpd_serve_cobbler_files --> off

<truncated>

There are quite a lot of these, and far more are available for other daemons.  The boolean we are looking for is highlighted in the output above, but we needn’t have guessed it as the error message above actually told us which one to toggle.

setsebool -P httpd_read_user_content 1

This will set the boolean to 1 or on.  The -P option tells setsebool to make this change a permanent one.  This will, in fact, solve the problem.  But what did this command actually do?

We may check the potential effects of an SELinux boolean with the sesearch command:

# sesearch -b httpd_read_user_content -AC

Found 15 semantic av rules:

DT allow httpd_suexec_t home_root_t : dir { getattr search open } ; [ httpd_read_user_content ]

DT allow httpd_suexec_t home_root_t : lnk_file { read getattr } ; [ httpd_read_user_content ]

<truncated>

Since SELinux operates as a whitelist (default deny, or paranoid), we are most interested in any new access that will be granted by the boolean.

Above, we instructed sesearch to retrieve conditional access rules for the httpd_read_user_content boolean; 15 rules were enabled by this boolean.  Checking the effects of booleans before switching them on is a good security practice.

Task 2

Our second task was to change the document root for http from /var/www/html to a new directory: /web.

First, we create the directory, then set and check permissions:

# ls -ldZ /web

drwxr-xr-x. root root unconfined_u:object_r:default_t:s0 /web

After altering the httpd.conf file to point to the new document root and restarting the httpd service, we verify our work. 

When we browse to the website’s index page, we see this:

Forbidden

You don't have permission to access /index.html on this server.

Setting SELinux to permissive mode results in success.  Why is SELinux blocking?  Let’s examine the logs.  Last time, we checked /var/log/messages.  This time, we will check at /var/log/audit/audit.log.

This file is technically human readable, but approaching it with tools like grep and less can be frustrating.  The lines are very long and full of obscure data.  A better tool might be ausearch:

# ausearch -i -m avc -c httpd -ts today | tail -1

type=AVC msg=audit(07/25/2017 10:37:41.325:1055) : avc: denied  { read } for  pid=8113 comm=httpd name=index.html dev=dm-0 ino=392525 scontext=unconfined_u:system_r:httpd_t:s0 tcontext=unconfined_u:object_r:user_home_t:s0 tclass=file

The command above translates to: “Fetch any AVC (Access Vector Cache – basically SELinux) messages related to the common name “httpd” which occurred sometime today, and trim that list to only show the last entry.  Also, please translate as many ID numbers as you can into the names of the things they represent.”

The results are still somewhat difficult to read, but present a significant improvement over the raw logs.  We’ve highlighted some notable entries in the output above.  From these, we can determine that:

*   SELinux blocked httpd from interacting with /web/index.html
*   The security context it was coming from was: system_u:system_r:httpd_t:s0
*   The security context it was targeting was: unconfined_u:object_r:default_t:s0

It seems that our current policy doesn’t allow the httpd_t domain to access files of the type default_t.  We know from earlier testing that SELinux was not blocking access to files in /var/www/html. 

Let’s check the context for those files.

# ls -Z /var/www/html

-rw-r--r--. root root unconfined_u:object_r:httpd_sys_content_t:s0 index.html

We can compare this to the context for files in /web:

# ls -Z /web

-rw-r--r--. root root unconfined_u:object_r:default_t:s0 index.html

It seems that the types do not match.  SELinux is treating interactions between httpd_t and httpd_sys_content_t differently than those between httpd_t and default_t.

We can ask SELinux about these rules with the sesearch command.  The invocations of sesearch below use the following options:

*   --rule – type of rule sought:  allow, type, neverallow, audit, dontaudit, etc.
*   -s – the source domain, i.e. the domain attempting to interact
*   -t – the target; the domain or object being interacted with
*   -c – the class of object: file, dir, socket, file system, etc.
*   -p – permission type: read, write, ioctl, create, etc.

Let’s start by asking it what sorts of permissions the httpd_t domain has against httpd_sys_content_t:

# sesearch --allow -s httpd_t -t httpd_sys_content_t

Found 13 semantic av rules:

allow httpd_t httpd_sys_content_t : file { ioctl read getattr lock open } ;

<truncated>

Above is an access rule which allows processes in the httpd_t domain several permissions against files of the httpd_sys_content_t type.  Let’s ask a similar question regarding interactions between httpd_t and default_t.

# sesearch --allow -s httpd_t -t default_t

Found 3 semantic av rules:

allow domain base_file_type : dir { getattr search open } ;

allow httpd_t file_type : file system getattr ;

allow httpd_t file_type : dir { getattr search open } ;

Now we have some idea what the problem is.  The httpd_t domain doesn’t have any access defined for files in the default_t domain.

We could change our system policy to allow that interaction, but doing so would then allow httpd_t to have access and permissions on any other files sharing the default_t type.  This isn’t especially desirable.  The easiest and most secure way to fix this issue is to assign the httpd_sys_content_t type to the /web directory (and the files created underneath it).

We can do this with the semanage tool.  The specific thing we wish to change is the file context or “fcontext” for short.  We can ask semanage to list the file contexts that it knows about by using semanage -l.  This will be an enormous list, so we will want to filter it for the specific directories or types that we are interested in with grep:

# semanage fcontext -l | grep /var/www

/var/www(/.*)?    all files   system_u:object_r:httpd_sys_content_t:s0

The command above returned 49 results on the example server.  We have only included the relevant result for consideration.  Take note of this portion: /var/www(/.*)?   
This is a regular expression.  We will have much more to say about these in a later module.  This particular expression is defining a match for:

*   Any filenames which start with: /var/www
*   AND are followed by ONE or ZERO matches of:
*   / followed by
*   Anything or nothing.

Another way to say this is: /var/www and everything under it.

This is called a default file context. The default file contexts for every file in the targeted environment should be located in the /etc/selinux/targeted/contexts/files/ directory.  Two files here are especially interesting: file_contexts and (if it exists) file_contexts.local.

On a test server, file_contexts contained 4638 lines.  If we added a context to a new file, it would be recorded in file_contexts.local.

We’ve determined that we need to alter the context of the /web directory (and its contents) to match that of the /var/www/html directory.  To do that, we will use semanage:

# semanage fcontext -a -t httpd_sys_content_t /web"(/.*)?"

# cat file_contexts.local

# This file is auto-generated by libsemanage

# Do not edit directly.

/web(/.*)?    system_u:object_r:httpd_sys_content_t:s0

Above, we’ve instructed semanage to set the file context for /web and all files beneath it to httpd_sys_content_t.  We then verified this by checking the contents of file_contexts.local.  However, checking the context of the /web directory reveals a problem:

# ls -Z /web

-rw-r--r--. root root unconfined_u:object_r:default_t:s0 index.html

The context has not changed.  This is because the security context for files is stored as metadata inside a file’s inode.  We can see it with stat:

# stat /web/index.html

File: ‘/web/index.html’

<truncated>

Context: unconfined_u:object_r:default_t:s0

Access: 2017-07-06 09:56:05.496127360 -0500

Modify: 2017-07-06 09:17:18.079419449 -0500

Change: 2017-07-06 09:17:18.079419449 -0500

Birth: -

Our actions so far have not affected the stored context in the inode; instead, the information in file_contexts.local represents only what we intend the context to be.  To apply the intended context to the file we will use restorecon:

# restorecon -vR /web

restorecon reset /web context

unconfined_u:object_r:default_t:s0-> unconfined_u:object_r:httpd_sys_content_t:s0

restorecon reset /web/index.html context unconfined_u:object_r:default_t:s0-> unconfined_u:object_r:httpd_sys_content_t:s0

Above, we instructed restorecon to restore our intended contexts to the /web directory and everything beneath it.  The verbose output tells us precisely what the command accomplished.  We can verify this with ls -Z:

# ls -Z /web

-rw-r--r--. root root unconfined_u:object_r:httpd_sys_content_t:s0 index.html

Testing the website again now displays index.html as intended.  If we should like to remove this custom context, we may do so by passing the -d option to semanage as below:

semanage fcontext -d "/web(/.*)?"

This will remove the line from file_contexts.local, but we will still need to run restorecon to apply the changes.

A final note regarding file contexts:  some directories defined in the default contexts contain many and various type definitions for the sorts of files that would logically be created inside of them.  It may not be sufficient, therefore, to simply match the label of a top level directory like /web to the label of /var/www.

In cases like these, we may use the concept of equivalency to resolve the disparity.  We can use semanage to accomplish this:

# semanage fcontext -a -e /var/www /web

# restorecon -Rv /web

This tells SELinux to treat /web as if it were /var/www for the purposes of labeling going forward.

Task 3

The third task in our example scenario was to change the port that httpd listens on, from 80 to 8000.  After changing the configuration file so that httpd will listen on 8000, we attempt to restart the service:

# service httpd restart

Stopping httpd:                                            [  OK  ]

Starting httpd: (13)Permission denied: make_sock: could not bind to address [::]:8000

(13)Permission denied: make_sock: could not bind to address 0.0.0.0:8000

no listening sockets available, shutting down

Unable to open logs

[FAILED]

From the output above, we can deduce that the failure was the result of a denied permission.  We can’t be sure from the output, but it might an SELinux access problem.  We can be more sure if we briefly place SELinux into Permissive mode and attempt to start the service again:

# setenforce 0

# service httpd restart

Stopping httpd:                                            [  OK  ]

Starting httpd:                                            [  OK  ]

The commands completed with no errors.  Time to check the audit logs (and place the system back into Enforcing mode!).  Let’s try that ausearch command from earlier again:

# ausearch -i -m avc -c httpd -ts today | tail -1

type=AVC msg=audit(07/25/2017 15:09:15.737:1273) : avc:  denied  { name_bind } for  pid=9085 comm=httpd src=8000 scontext=unconfined_u:system_r:httpd_t:s0 tcontext=system_u:object_r:soundd_port_t:s0 tclass=tcp_socket

This confirms for us that httpd was not allowed to bind to TCP 8000.  We stated earlier in this module that SELinux assigns types to ports as well as other resources.  We can get a list of ports that SELinux knows about by asking semanage port -l.  This will be a lengthy list – since we’re primarily interested in the http protocol, we’ll filter that down with grep:

# semanage port -l | grep http

http_cache_port_t    tcp      8080, 8118, 8123, 10001-10010

http_cache_port_t    udp      3130

http_port_t          tcp      80, 81, 443, 488, 8008, 8009, 8443, 9000

pegasus_http_port_t  tcp      5988

pegasus_https_port_t tcp      5989

It seems that 8000 is not one of the defined, allowable ports for http.  We can add it to the list if we wish, but we should first check to make sure that 8000 isn’t already defined for another service:

# semanage port -l | grep 8000

soundd_port_t                  tcp      8000, 9433, 16001

TCP port 8000 is already defined for soundd_port_t.  We have no plans to ever enable soundd on this server, but SELinux policy has defined the context for 8000.  The best we can do here (unless we want to create a policy module and recompile) is to use the -m switch of semanage port to modify the record:

# semanage port -m -t http_port_t -p tcp 8000

# semanage port -l | grep 8000

http_port_t                    tcp      8000, 80, 81, 443, 488 …

soundd_port_t                  tcp      8000, 9433, 16001

This will allow httpd to start and bind to port 8000:

# netstat -tlnp | grep 8000

tcp        0      0 :::8000                     :::*                        LISTEN      9088/httpd

We have succeeded.  For future purposes, perhaps it would be a good idea to check whether a given port has been assigned a context before designating it as an off-label prescription for a standard protocol. 

Exploring Type Transition Rules

To this point in our discussion of Type Enforcement, our focus has revolved around access rules.  While access rules are critically important, they are not the only policy tools in our kit.

Earlier, we noted that domains may interact with one another, and that these interactions could be controlled with policy.  This naturally leads us to a discussion of a type of enforcement rule known as a type transition.

It might be helpful to see the effects of these rules before attempting to define them. 

Let’s start by examining the security context label for /usr/bin/passwd (a command that allows users to change their own passwords):

# ls -Z /usr/bin/passwd

-rwsr-xr-x. root root system_u:object_r:passwd_exec_t:s0 /usr/bin/passwd

The piece we are most interested in is the type (highlighted above).  The passwd executable has a type of passwd_exec_t.  We might also note that it has been assigned a role of object_r.

Earlier, we stated that processes are subjects (as opposed to objects), and that processes are assigned to domains.  Here is an executable, but the context has labeled it an object.  Is the label incorrect?  No, the context is correct.  That is because /usr/bin/passwd is a file.  Executing it causes a process to be spawned.  The process and the file that initiated it are treated differently.

To demonstrate this, let’s call the passwd command and park it in the background:

# /usr/bin/passwd &

[1] 48261

# Changing password for user root.

[1]+  Stopped                 passwd

# ps -eZ |grep passwd

unconfined_u:unconfined_r:passwd_t:s0-s0:c0.c1023 48261 pts/0 passwd

Notice the change in type.  The process has a type of passwd_t.  It seems that SELinux has permitted us to execute a file with a type of passwd_exec_t; but, when that file executed, the process it spawned did NOT inherit the passwd_exec_t type.  Instead, it was brought under the passwd_t domain. 

Let’s use the sesearch tool to pull relevant transition rules out of our policy.  First, we’ll check our own security context:

# id -Z

unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023

We’re in unconfined_t.

Let’s see what sorts of type_transition rules exist from unconfined_t to passwd_exec_t.

# sesearch --type -s unconfined_t -t passwd_exec_t

Found 1 semantic te rules:

 type_transition unconfined_t passwd_exec_t : process passwd_t;

This is the rule we’re looking for.  We can read it this way:

*   type_transition – this is a type transition rule
*   unconfined_t – source
*   passwd_exec_t – target
*   process – if starting a process
*   passwd_t – put spawned process under this domain

Or, to put it simply, “If unconfined_t starts a process using an executable typed as passwd_exec_t, run that process under passwd_t”.

Note that this rule doesn’t define whether unconfined_t can start such a process; it only defines what happens when it does.  In order for this transition to occur, several other rules would have to exist. 

Specifically:

*   The target file type would need to be executable in unconfined_t:

# sesearch --allow -s unconfined_t -t passwd_exec_t -p execute

allow unconfined_t passwd_exec_t : file { read getattr execute open } ;

*   The passwd_t domain must define an entry point for passwd_exec_t:

# sesearch --allow -s passwd_t -t passwd_exec_t -p entrypoint

allow passwd_t passwd_exec_t : file { ioctl read getattr lock execute execute_no_trans entrypoint open } ;

*   The new process needs permission to transition into passwd_t:

# sesearch --allow -s unconfined_t -t passwd_t -p transition

 allow unconfined_t passwd_t : process transition ;

The syntax for these rules can seem daunting at first.  Practice and time spent with the sesearch man pages is the best prescription. 

Moving and Copying Files in SELinux

Moving and copying files in SELinux presents additional considerations beyond what we would see on an unsecured system.  This is because of the security context, or labels assigned to files. 

You may recall from the file system module that moving a file is actually a directory operation.  We do not copy data from one place to another (unless we moved the file to a new file system).  Rather, we simply change the referring entries in the appropriate directories. 

Labels are stored in a file’s inode, and they will not be updated by a move.  This is also why files retain ownership and standard permissions metadata when moved in a classic system.

Copying, on the other hand, results in the creation of a new file, and therefore, a newly populated inode with new metadata.  This new file will be assigned a label based on the defined contexts of the directory it inhabits.

Passing the -Z option to cp or mv will cause one to behave like the other regarding labels.  That is to say:

*   cp -Z will assign the file context of the original file to the new file, and,
*   mv -Z will caused the moved file to change its context to the defaults for its new location.

Often, when SELinux problems occur, it is because we failed to account for these behaviors.

Creating Policy with audit2allow

When all of the aforementioned techniques have been tried and tested, but SELinux issues still persist, there is a tool that we can use to resolve policy errors.  This tool is called audit2allow, and it should be used sparingly, if at all.

This is because audit2allow will take, as input, AVC error messages from the audit log.  It will then transform these error messages into policy modules which will allow the blocked behavior.  The tool is so powerful, that it may take the entirety of /var/log/audit/audit.log as input, and generate a policy module which will allow all of the blocked behaviors.

We will briefly demonstrate this by running audit2allow against the errors generated in our httpd scenario from earlier:

# cat /var/log/audit/audit.log | grep AVC | grep denied | audit2allow -o /test/source.te

# cat /test/source.te

#============= httpd_t ==============

#!!!! WARNING: 'default_t' is a base type.

#!!!! The file '/web/index.html' is mislabeled on your system.

#!!!! Fix with $ restorecon -R -v /web/index.html

allow httpd_t default_t:file { getattr open read };

#!!!! This avc is allowed in the current policy

allow httpd_t httpd_user_content_t:dir read;

allow httpd_t soundd_port_t:tcp_socket name_bind;

#!!!! This avc is allowed in the current policy

allow httpd_t user_home_t:file { open read };

Above, we used the -o option to generate an uncompiled source for reading.  This has not been applied to policy.

The lines starting with allow are the proposed rules.  The lines starting with #!!!! are audit2allow attempting to get us to see reason.  For example:

#!!!! WARNING: 'default_t' is a base type.

#!!!! The file '/web/index.html' is mislabeled on your system.

#!!!! Fix with $ restorecon -R -v /web/index.html

allow httpd_t default_t:file { getattr open read };

Here, audit2allow is telling us that we are about to grant httpd_t file permissions on anything of the default_t type.  This is nonsensical. 

“Why not fix this with restorecon?” asks audit2allow.  In the other sections, audit2allow excitedly warns us that our current policy settings aren’t even causing these exceptions anymore.  The tool does its best to guide us down the path of righteousness, but if we so choose, we may persist in reckless folly.  Here is the command from before, but with the -M option:

# cat /var/log/audit/audit.log | grep AVC | grep denied | audit2allow -M bad_idea01

******************** IMPORTANT ***********************

To make this policy package active, execute:

semodule -i bad_idea01.pp

Now we’ve created a compiled policy module.  We may load it in, as noted above, with semodule -i bad_idea01.pp.

Of course, we won’t do this.  But, if we had (and only later realized our mistake), we could disable this module with:

semodule -d bad_idea01

One final thing worth noting:  some SELinux rules prevent logging of activities to the audit log.  This is not malicious behavior; rather, it is simply designed to stop certain frequent and innocuous occurrences from spamming the logs.  If we would like to turn on auditing temporarily for everything that may be audited, we may do so like this:

semodule -DB

If we would like to disable this behavior again, we would do this:

semodule -B

SELinux Configuration

We have previously covered the use of the setenforce command to flip SELinux into and out of the enforcing state.  SELinux can be configured in 3 states. They are:

*   Enforcing – selinux is active and enforcing policy
*   Permissive –selinux logs policy exceptions, but does not enforce
*   Disabled – selinux is disabled in the kernel

The type of enforcement may also be set.  Some of these are:

*   Targeted – system default, important processes are protected
*   Minimum – like targeted, with a smaller selection of targets
*   MLS – Multi Level Security

As a quick refresher, recall that we can determine the current state of SELinux with getenforce and we can change the state to “Permissive” (and back again) using setenforce. The “Permissive” state does not disable SELinux.  Rather, it puts SELinux into a passive, audit-only mode.  Logs will still be generated, but access will not be confined.  To disable SELinux (that is, to boot without loading the SELinux module at all), we must alter /etc/selinux/config:

# This file controls the state of SELinux on the system.

# SELINUX= can take one of these three values:

#     enforcing - SELinux security policy is enforced.

#     permissive - SELinux prints warnings instead of enforcing.

#     disabled - No SELinux policy is loaded.

SELINUX=enforcing

# SELINUXTYPE= can take one of three two values:

#     targeted - Targeted processes are protected,

#     minimum - Modification of targeted policy. Only selected processes are protected.

#     mls - Multi Level Security protection.

SELINUXTYPE=targeted

In the emphasized portion of the output above, we can see two important options for configuring SELinux on our system.  The first is the enforcement state.  We have shown how to configure this on a running system, but this value would be overwritten at next boot by the value listed in /etc/selinux/config. 

The second is the SELINUXTYPE.  This defines the behavior of SELinux when it is enforcing.  The default enforcement type on SELinux systems is “targeted”.  This simply means that most common system services will operate in a confined domain.  “Minimum” represents a smaller set of services, but otherwise operates similarly to “targeted”.

A quick word about autorelabeling

If SELinux has been disabled on a system, and we now wish to enable it, we should ensure that all files on the system are properly labeled.  Failure to do so will certainly result in errors. 

To accomplish a full system relabel, we will need to create a single, empty file in the / directory: autorelabel.

# touch /.autorelabel

When the system next boots, it will automatically relabel our file systems and files.

Module 13:
Networking

EL6 represents a transitional period in the control of networking.  While network configuration can be done through manual editing of files, EL6 does provide some easier to use tools for managing simple configurations.  These may or may not be available, so having the knowledge to perform a full manual configuration is best.

NetworkManager, nm-applet

The first simple tool to address is provided through the NetworkManager service.  If you are using a graphical interface, the NetworkManager gui nm-applet and the NetworkManager service should be running.  The icon that brings up nm-applet is normally either in the top right corner of your screen, next to the date; or under the System, Preferences menu.  If it is not running you can invoke it from a terminal within the gui: #nm-applet &. 

If you use nm-applet for configuration, do not edit any files manually as the changes will not be communicated to NetworkManager.  Also any changes made via nm-applet will overwrite or even erase the configuration files completely!  NetworkManager is generally accepted as the best tool if you are using a DHCP-only computer, one which is irregularly connected, or one which uses wireless. 

In EL7 NetworkManager and its companion command line tool nmcli is the best tool for the job, and is fully featured.  But in EL6 command line support has not matured and many administrators dispense with NetworkManager entirely.  If you choose not to use NetworkManager, it should be stopped, disabled, and removed before you do any configuration.  This will keep it from interfering with things.  Then the default network service should be enabled:
#service NetworkManager stop ; chkconfig NetworkManager off
#yum -y remove NetworkManager*
#service network start ; chkconfig network on.

system-config-network

The second tool is less problematic than NetworkManager as all it really does is edit the files that you would otherwise manually configure yourself.  To access a simple text user interface, simply type system-config-network.  After making the appropriate changes, save and exit.  Network changes will take effect after service network restart.  Hostname changes will not apply until after a reboot.

/etc/sysconfig/network & ifcfg-ethX

For basic network config you will need to edit a couple of files.  First set your hostname.  The traditional file /etc/hostname is ignored in EL6, instead edit /etc/sysconfig/network.  This file contains global settings and should have at least two lines:
NETWORKING=yes
HOSTNAME=server-name.domain.dom.

The only other useful directives that could be added to this file are GATEWAY=IP, which sets the gateway; and GATEWAYDEV=ethX, which is used in multi-NIC installations to define a preferred route to the gateway.  It is generally considered best practice to set the gateway at the interface level instead.

Next edit /etc/sysconfig/network-scripts/ifcfg-ethX, where X is the interface number.  The first network card number is 0.

A minimal static configuration should look like this:

DEVICE=eth0

TYPE=Ethernet

ONBOOT=yes

NM_CONTROLLED=no

USERCTL=no

BOOTPROTO=static

IPADDR=10.10.10.10

NETMASK=255.255.255.0

GATEWAY=10.10.10.1

DNS1=8.8.8.8

DNS2=8.8.4.4

Some notes about the directives:

*   DEVICE – specifies what we are configuring
*   HWADDR – optional, but best practice.  Keeps the network service from becoming confused if a NIC moves or initializes in a different order.
*   ONBOOT – should we start this when we boot?
*   NM_CONTROLLED – prevents NetworkManager from touching the interface.
*   USERCTL – prevents non-root users from modifying the interface
*   BOOTPROTO – dhcp is also an option
*   IPADDR / NETMASK / GATEWAY / DNS – self-explanatory. 

    *   If assigning multiple IPs use IPADDR0 / NETMASK0 / GATEWAY0, IPADDR1, etc…
    *   If you prefer using CIDR, you can use PREFIX instead of NETMASK
*   PEERDNS – if set to yes, this file will write to /etc/resolv.conf, default for dhcp interfaces

The network interface number is recorded in /etc/udev/rules.d/70-persistent-net.rules.  When an EL6 virtual machine is cloned, or migrated, it will often 'remember' the old interface.  To resolve this, simply cat /dev/null into the file.

Full documentation of this file and other related files can be found at /usr/share/doc/initscripts-version/sysconfig.txt.

After altering the configuration file, the network service or the interface must be restarted for the changes to take effect.  To individually manipulate an interface you can use the commands ifup and ifdown followed by the interface name.

hosts, nsswitch.conf & resolv.conf;  ip, ifconfig & route

The file /etc/hosts holds static entries for hostname resolution.  It should be modified to contain the hostname like this:

127.0.0.1   localhost.localdomain                server-name

::1         localhost.localdomain   localhost6   server-name

Address and hostname combinations can also be added to /etc/hosts. This is often done because the name in question is not served by a dns server (as in a test network), to provide faster resolution, or for redundancy in case of dns or network failure.  If you do add entries to the hosts file, remember that when an address changes, you must manually change the host file with it.

The default order of hostname resolution is /etc/hosts (known as files) then dns.  If there is a need to reverse this order, change the hosts: line in /etc/nsswitch.conf.  Be careful when doing this, as nsswitch.conf is consulted by many other processes, including authentication.

DNS servers for the computer can be configured in /etc/resolv.conf (yes, it's missing the e), using the nameserver directive.  The search directive can also be used to define a name search space.  This is useful for single name host resolution.  Settings in resolv.conf are overridden by those specified in an interface configuration script.

Current network configuration can be viewed using ifconfig, or with ip a.  Routing table information is available using either ip route, or simply route.  While these commands have historically been used to configure interfaces and change the routing table, they should no longer be used in this way.  They should only be used to view information.

To view and manipulate the address resolution tables (arp for IPv4 and ndisc for IPv6) use ip neighbor. 

netstat and ss

For diagnosis of TCP/IP ports, operations, and states, two tools are employed:

*   netstat, though its use is deprecated on most modern systems. 
*   ss, which is seen largely as an enhancement of and replacement for the netstat command.

The functionality of netstat, including common options, is built into ss.  We’ll begin with a discussion of netstat, and proceed from there into ss.

When using netstat, we are typically attempting to retrieve information about active tcp/udp ports or routing table contents.

To list active tcp ports, we would call netstat like this:

# netstat -at | tr -s [:space:]

Active Internet connections (servers and established)

Proto Recv-Q Send-Q Local Address Foreign Address State

tcp 0 0 *:5902 *:* LISTEN

tcp 0 0 *:sunrpc *:* LISTEN

tcp 0 0 localhost.localdomain:smtp *:* LISTEN

tcp 0 64 server.example.local:ssh 192.168.1.81:62329 ESTABLISHED

<truncated>

Let’s take a closer look at this line:

tcp 0 64 server.example.local:ssh 192.168.1.81:62329 ESTABLISHED

We can read this as:

*   tcp – the protocol in use
*   0 64 – packets queued in the receive and send buffers, respectively
*   server.example.local:ssh – our local address and , or the socket we receive on.  Here, netstat is displaying our hostname in place of ip address, and has replaced the well-known port number for ssh (22) with the friendly name “ssh”
*   192.168.1.81:62329 – the remote address and port, or socket the connecting entity is sending on
*   ESTABLISHED – the state of the port/connection; typically LISTEN or ESTABLISHED, but could list any of the valid TCP connection states

When we see asterisks in the output, they can be read as “ANY” or “ALL”.  Consider this line from the example output: tcp 0 0 *:5902 *:* LISTEN
Here, the first asterisk, *:5902, indicates that we are listening on all ip addresses available to the local machine (on port 5902).  The second set, *:*, indicates that we are listening for connections from any source IP and any source port.

To see routing table information, we would use netstat -nr (where n causes numerical addresses to display in place of symbolic names):

# netstat -nr

Destination      Gateway         Genmask         Flags   Iface

192.168.1.0      0.0.0.0         255.255.255.0   U       eth0

169.254.0.0      0.0.0.0         255.255.0.0     U       eth0

0.0.0.0          192.168.1.1     0.0.0.0         UG      eth0

Above, we can see the routing table stored in the kernel.  We can interperet the output like this:

*   Destination – the destination host or network.  0.0.0.0 indicates a default route.
*   Gateway – next local delivery point.  0.0.0.0 indicates local network.
*   Genmask – the network mask for this route
*   Flags – information about the route. U=Up, G=has gateway, H=single host route.
*   Iface – the exit interface applicable to this route.

In modern Linux, netstat has largely given way to ss.  ss provides us with all of the tools built into netstat, but has extended capabilities.  It retrieves information directly from the kernel, rather than reading the contents of /proc as netstat does.  It also includes a set of built-in filtering tools.  Let’s take a look at some of these:

# ss -ta state listening

Recv-Q Send-Q        Local Address:Port          Peer Address:Port

0      128             *:47428                         *:*

0      5               *:5901                          *:*

0      5               *:5902                          *:*

0      128             *:sunrpc                        *:*

0      128             *:ssh                           *:*

0      128           127.0.0.1:ipp                    *:*

0      100           127.0.0.1:smtp                   *:*

Here we’ve listed all tcp ports, which we could have done with netstat.  New with ss, however, is this portion: “state listening”.  This allowed us to filter output to only those ports currently in the LISTENING state. 

We can also filter on destination and source ports:

# ss -t4 state established src :22

Recv-Q Send-Q           Local Address:Port               Peer Address:Port

0      64               192.168.1.164:ssh                192.168.1.81:62329

Here we have asked for:

IPv4 TCP Ports
with a state of ESTABLISHED
and a source port of 22

Or, in other words, any established ssh sessions from a remote device to this server.

standard tools

While the way we configure networks has changed, most of the diagnostic tools have not:

*   ping – test connectivity
*   traceroute – print the path to a host
*   tracepath – like traceroute only using UDP, discovers MTU along the way
*   dig – do a DNS lookup, for instance:

    *   dig google.com NS – find google.com's name servers
    *   dig @ns1.google.com yahoo.com – ask google's name server for yahoo's address
    *   part of the bind-utils package, along with nslookup, host, and nsupdate.
*   nslookup – interactive DNS resolution tool, sub commands include:

    *   server – server to query
    *   set type= – query type, e.g.: A, PTR, MX, NS
*   whois – query a name registrar, installed as the jwhois package
*   curl / wget – non-interactive ways to download from a URL
*   ncat – the swiss-army knife for networking.  Can be used for lots of stuff
*   tcpdump – wire-level level listener/parser
*   netstat – show socket information, superseded by ss.  Useful switches include:

    *   -c – continuous
    *   -l – listening ports only
    *   -a – all ports
    *   -e – extended detail
    *   -t – TCP
    *   -u – UDP
    *   -p – show PID and program that owns the socket
    *   -n – numeric address only
    *   -s – statistics
*   ss – replaces netstat, which is deprecated.  Uses most of the same switches but adds:

    *   -m – memory usage
    *   -o – time
    *   state – taken with options such as established, syn-sent, syn-recv, connected
    *   src/dst – source or destination address (port optional)
    *   sport/dport = followed by source or destination port number (:443)

iptables

iptables is a utility which overlays the netfilter firewall built into the Linux kernel.  It defines rules for the handling or mangling of packets based on either stateless or stateful packet inspection.

The STIG says only that the iptables service must be running and set to run by default, and that the default action for both the INPUT and FORWARD chains should be set to DROP.  This results in a system which blocks ALL incoming communication by default, and permits only by exception (that is, explicitly defined rules).  It falls to local administrators to create the rules which will allow mission critical services to be accessed.

To check the status of iptables, we will use the service command.  When iptables is stopped this is the result:

# service iptables status

iptables: Firewall is not running.

When the service is running, a status check will print the current rulesets for each defined chain:

# service iptables status

Table: filter

Chain INPUT (policy ACCEPT)

num  target     prot opt source               destination

1    ACCEPT     all  --  0.0.0.0/0            0.0.0.0/0           state RELATED,ESTABLISHED

2    ACCEPT     icmp --  0.0.0.0/0            0.0.0.0/0

3    ACCEPT     all  --  0.0.0.0/0            0.0.0.0/0

4    ACCEPT     tcp  --  0.0.0.0/0            0.0.0.0/0           state NEW tcp dpt:22

5    ACCEPT     tcp  --  0.0.0.0/0            0.0.0.0/0           state NEW tcp dpt:8000

6    REJECT     all  --  0.0.0.0/0            0.0.0.0/0           reject-with icmp-host-prohibited

Chain FORWARD (policy ACCEPT)

num  target     prot opt source               destination

1    REJECT     all  --  0.0.0.0/0            0.0.0.0/0           reject-with icmp-host-prohibited

Chain OUTPUT (policy ACCEPT)

num  target     prot opt source               destination

We can use the chkconfig command to determine if iptables will be started at boot time, and if so, at which runlevels it will be executed.

# chkconfig --list iptables

iptables        0:off   1:off   2:on    3:on    4:on    5:on    6:off

Basics of iptables chains and rules

In this section, we will cover only the states, chains, tables, and rules necessary to configure iptables for use as a local host firewall.  Here is a brief set of terms to be familiar with:

*   Rule: defines a condition for matching packets, and typically a target.
*   Jump: located in the target portion of a rule, identifies a target to move handling to.
*   Target: the action part of a rule.  It defines how matched packets are to be handled.

    *   may be another chain, or a special value: ACCEPT, DROP, QUEUE, REJECT, or RETURN
*   Chain: a set of rules that work together to accomplish the purpose of the chain.
*   Table: the underlying software construct that provides fulfilment for defined rules.
*   State: the condition of a packet relative to other packets in a stream.  Possible states for a packet are NEW, ESTABLISHED, RELATED, or INVALID.  States will be discussed in more detail further on in this material.

iptables uses four tables to do its work: raw, nat, mangle, and filter.  Newer implementations use a fifth table, security, which enforces additional networking rules under SELinux.  Our focus will be on the filter table. 

There are three default chains in filter table: INPUT, OUTPUT, and FORWARD.  The STIG mandates security on the INPUT and FORWARD chains.  We will be creating rules in the INPUT and OUTPUT chains.  There is also a PREROUTING chain in the nat table which is used for connection tracking that powers state based inspection.  We won't be interacting with this chain directly.

We will walk through the creation of a small set of rules.  First, we’ll create a rule to drop incoming requests for http.  Then we’ll create default DROP policies for the INPUT and FORWARD chains.  Finally, we will create a rule that allows https and discuss the STATE portion of that rule.  Along the way, we will discuss how rules are implemented, and address some issues with an example chain.

We begin by checking iptables to see if a rule for http already exists:

# iptables -L | grep http

From this lack of output, we can see that no rule exists to explicitly allow or prohibit http.  We then create a rule specifically blocking it:

# iptables -I INPUT -p tcp --dport 80 -j DROP      

This can be read as:

*   -I INPUT – insert a rule into the INPUT chain. 

    *   By default, this will place the rule at the top of the chain.  Precise position within a chain can be specified numerically.  Other options here are:

        *   -A – append to the end of a chain
        *   -D – delete a rule based on position or content),
        *   -R – replace a rule based on position or content
        *   -F – flush all rules, emptying a chain
*   -p – protocol: tcp, udp, icmp, all
*   --dport – destination port.  In this case 80.
*   -j – jump to a target (DROP) or to another chain

Let’s look at the other rules in the input chain to see how this one will be implemented:

# iptables -L

Chain INPUT (policy ACCEPT)

target     prot opt source      destination

DROP       tcp  --  anywhere    anywhere      tcp dpt:http

ACCEPT     all  --  anywhere    anywhere

ACCEPT     tcp  --  anywhere    anywhere      state NEW tcp dpt:ssh

ACCEPT     tcp  --  anywhere    anywhere      state NEW tcp dpt:irdmi

REJECT     all  --  anywhere    anywhere      reject-with icmp-host-prohibited

At first glance, there appear to be some problems here.  Specifically, the second rule:

ACCEPT     all  --  anywhere    anywhere

This rule appears to match all incoming packets and ACCEPT them.  This is misleading, for reasons we’ll return to in a moment.  To understand the apparent problem, let's take a moment to discuss how iptables rules are read and implemented in the INPUT chain.

1.  A packet arrives on an interface (this is important), destined for a local service.
2.  The INPUT chain is consulted, and the rules inside are run against the packet.
3.  The rules are read in order, from top to bottom.
4.  If a match is found, the actions dictated by the rules inside the INPUT chain are performed. 

    1.  Processing stops when a match is made.
    2.  The default policy acts as the final rule which matches all packets.
5.  The packet is accepted, dropped, rejected, or passed to another chain for processing.

    1.  If the packet was dropped, it will simply disappear.  Neither the sender nor the receiving host will be notified.
    2.  If the packet is rejected, the sender will be notified through the specified channels that the rejection has occurred.
    3.  If the packet was accepted, it is then passed to the local destination service.

This is slightly simplified, but this serves as a framework for understanding the process.  We should now understand why a rule which accepts all packets for would nullify any rules following it.  Processing would stop after the match.  In this case, however, we are missing a critical piece of information.  Using the -v option yields more detail about the rule:

# iptables -L -v

Chain INPUT (policy ACCEPT 0 packets, 0 bytes)

pkts bytes target   prot opt in   out  source      destination

<truncated>

    0     0 ACCEPT   all  --  lo   any  anywhere    anywhere

Specifically, it now lists which interface the rule applies to.  In this case, it only applies to our loopback adapter.  Packets arriving on our external interfaces will not be affected by this rule.  When inspecting rules, remember to include interfaces in the output!  From this point forward, any rules we discuss will be applied to all interfaces. 

Returning to our examination, the first rule is the one we created earlier.  It will drop packets destined for port 80 (http) on this host.

target     prot opt source      destination

DROP       tcp  --  anywhere    anywhere      tcp dpt:http

Next we have these two rules:

ACCEPT     tcp  --  anywhere    anywhere      state NEW tcp dpt:ssh

ACCEPT     tcp  --  anywhere    anywhere      state NEW tcp dpt:irdmi

These rules allow new connections to our server for specific protocols: ssh and irdmi. 

Finally, at the end of the chain, we have this rule:

REJECT   all -- anywhere   anywhere   reject-with icmp-host-prohibited

This rule will REJECT any packet, and respond to the sending host using ICMP with the message: Destination Host Prohibited.  This rule is particularly interesting, because it serves as a final catch-all for any packets that weren’t matched in prior rules.  This rule is an explicit  “default deny”.  Is this rule necessary?  Looking at the first line of the configuration: Chain INPUT (policy ACCEPT).  The policy of the INPUT chain is ACCEPT.

Policies define the default implicit action a chain will take on any packets that aren’t matched by the rules of that chain.  In this context, an explicit rule is one that is written and appears literally in the rules for a chain.  An implicit rule is not literally stated, and serves instead as a default action that takes place invisibly.

If there were no other rules in this chain, nothing would be blocked.  With the presence of an explicit match-all REJECT rule at the bottom of our chain, this policy will never be enforced.  Instead, all otherwise unmatched packets will be matched by this rule, and summarily rejected.

This configuration presents some security concerns.  One of these is that, should an administrator inadvertently modify or delete the explicit rule, then the ACCEPT all policy of the chain will result in undesired connections to our server.  Another is that the REJECT target will respond to disallowed requests.  If an adversary were to run a ping sweep or port scan against this server, it would respond – confirming its existence as a possible target.

For this reason the INPUT and FORWARD chains must have a default policy of DROP.  This is accomplished with:

# iptables --policy INPUT DROP

The policy is now set to DROP, as mandated by STIG.  However, there is still a problem:

# iptables -L

Chain INPUT (policy DROP)

<truncated>

REJECT   all -- anywhere   anywhere   reject-with icmp-host-prohibited

Until the REJECT rule is removed, our default policy will never be enacted.  We can either remove the rule entirely and rely on the implicit DROP from policy, or replace the existing rule with an explicit DROP rather than REJECT.  The replacement with DROP is preferred, but not mandated.

Either way we will need to find the line number of the rule:

# iptables -L INPUT --line-numbers | grep REJECT

7 REJECT  all -- anywhere  anywhere  reject-with icmp-host-prohibited

To remove the rule:

# iptables -D INPUT 7

To modify (replace) this rule, we would use the -R option:

# iptables -R INPUT 7 -j DROP

# iptables -L INPUT 7

DROP       all  --  anywhere             anywhere

Above, we replaced the rule at position 7 with a DROP rule.  Since we did not specify source, destination, protocol, interface, port, or other details, the defaults were taken, and all packets, from and to anywhere on all interfaces will be matched. 

To conclude our experimentation with rules, we will create a rule explicitly allowing https connections to our server from an internal network only.  This rule will incorporate two new ideas: states and source/destination filtering. 

iptables is sometimes described as “stateful”.  What this means is that iptables can determine the relationship between packets in a stream.  These packets are then assigned a state based on that determination.  Possible states are:

*   NEW – A packet initiating a connection, such as an HTTP request.
*   ESTABLISHED – Part of an existing connection.
*   RELATED – A packet requesting a new connection but related to an existing connection. For example, FTP uses port 21 to establish a connection, but data is transferred on a different port, usually 20.
*   INVALID – A packet that is not part of any connection in the tracking table.

In order to initiate and maintain an incoming connection, a rule must allow at least NEW and ESTABLISHED states.  For some protocols, RELATED is also required.  It would be nonsensical to allow only NEW packets, as any following packets in that stream would be dropped, and a connection would never be allowed to form.  Given this, it is a common practice to place the following rule at or very near the top of the INPUT chain:

# iptables -I INPUT 2 -m state --state RELATED,ESTABLISHED -j ACCEPT

This results in the addition of a rule to the INPUT chain:

ACCEPT   all  --  anywhere   anywhere  state RELATED,ESTABLISHED

This rule will ACCEPT packets that are part of existing streams without further processing.  Thus we need only create rules that apply to NEW connections, simplifying the creation of rules, the complexity of the chain overall, and the overhead of inspecting established streams.

As we would also like to limit https connections to a single internal network, we must also specify an allowed source.  Rules can be configured to allow traffic from a given host, a single network, or a range of networks.  In the following example, we will choose the network 192.168.1.0 /24.

Let’s create the rule now:

iptables -I INPUT 6 -s 192.168.1.0/24 -m state --state NEW -p tcp --dport 443 -j ACCEPT

Note here the -m option, which allows for extended matching (in this case, against packet state), and the --state option which allows us to match against specific packet states (NEW).  Also note the new -s option, which specifies a source to match against (in this case, the entire 192.168.1.0/24 network).

Source and destination filtering control which networks and hosts are allowed to communicate across the firewall.  When iptables is acting as a host-based firewall, we would typically use source filtering on the INPUT chain (controlling which hosts and networks can reach our server) and destination filtering on the OUTPUT chain to control which networks our host may communicate with externally.

The file /etc/sysconfig/iptables holds the configuration applied when iptables starts.  On our example server it looks like this:

# Generated by iptables-save v1.4.7 on Wed Aug 16 16:30:11 2017

*filter

:INPUT DROP [0:0]

:FORWARD ACCEPT [0:0]

:OUTPUT ACCEPT [120:15888]

-A INPUT -p tcp -m tcp --dport 80 -j DROP

-A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT

-A INPUT -p icmp -j ACCEPT

-A INPUT -i lo -j ACCEPT

-A INPUT -p tcp -m state --state NEW -m tcp --dport 22 -j ACCEPT

-A INPUT -p tcp -m state --state NEW -m tcp --dport 8000 -j ACCEPT

-A INPUT -p tcp -m state --state NEW -m tcp --dport 443 -j ACCEPT

-A INPUT -j DROP

-A FORWARD -j REJECT --reject-with icmp-host-prohibited

COMMIT

Note the policy configuration for the INPUT chain has been changed to DROP by our earlier work.  Further, note the word COMMIT at the bottom of the file.  This is necessary for the configuration to be applied, and should not be removed or altered.  Finally, notice this line at the top of the file:

# Generated by iptables-save v1.4.7 on Wed Aug 16 16:30:11 2017

This line indicates that /etc/sysconfig/iptables was created by the iptables-save command.  Rather than invoking that command directly, we would typically perform this command instead:

# service iptables save

iptables: Saving firewall rules to /etc/sysconfig/iptables:[  OK  ]

This invokes the save() function from within the /etc/rc/d/init.d/iptables script.  This is a recommended practice, as many variants of iptables exist, and the scripts on your system will be tailored to your specific version.

This will also result in the creation of a second file, /etc/sysconfig/iptables.save.  This is a backup of whatever was in the iptables file prior to running the service iptables save command.

By default, when the iptables service is stopped or restarted, any rules added since the last save will be flushed.  This behavior can be modified by editing /etc/sysconfig/iptables-config, altering the IPTABLES_SAVE_ON_STOP and IPTABLES_SAVE_ON_RESTART directives.

We can modify /etc/sysconfig/iptables directly, if we choose.  This is, in fact, a common practice.  We recommend against it, and instead suggest that backups be made before any modifications, and that the commands provided by iptables be used to configure firewall rules.

It is worth noting that applications exist as an alternative to manually configuring the firewall with iptables.  Typically they are only a simplified interface passing commands to iptables.  One such application is the system-config-firewall tool.  This tool is available in EL6, but it should not be used if any manual configuration of iptables is performed, as it will overwrite or discard your changes.

Module 14: 
Installing Software

yum, repos, createrepo

EL6 comes with rpm, the RedHat Package Manager, as the primary way to install, manage, upgrade, and remove software.  It will work with software either in the rpm binary format or with compiled files with an attached plain-text manifest file.  It can install files from local storage or from an ftp or web site.  rpm is fully capable of performing everything you might ever need to do with software on a EL6 system, but it can be very tedious to use.  This is especially true when dealing with dependencies, which rpm can detect; but will not download or install automatically.  It also lacks the ability to automatically update a system. 

To make up for the shortfalls of rpm, yum was written.  It is a higher-level package manager that greatly simplifies the common software management tasks.  There are a few things that still need to be accomplished using rpm, but there aren't many. 

In future versions of EL, it is likely that yum will be supplanted by dnf, which is a fork/rewrite of yum with the same functionality and command structure.  There is also another common software manager: PackageKit, which overlays yum.  PackageKit is primarily designed as a graphical front end for end-users and is usually not installed on servers.

When using rpm you must locate software packages individually; yum uses collections of software known as repos (or repositories).  Your system will come with multiple Internet-based repos configured.  There is a prebuilt repo on most installation media, which can be used for software installation on isolated networks.  You can even create your own using createrepo on a directory full of rpm files. 

To obtain a list of available repos use yum repolist enabled.  To see installed packages yum list installed.  To figure out what package should be used for a given install: yum search keyword and yum provides program.  Detailed information can be obtained using: 
yum info packagename.  The repoquery command can list files in a package (-l), show capabilities provided (--provides), or find dependencies (--whatrequires).

Repo configuration files are stored in /etc/yum.repos.d/.  To use a custom repo:

*   Disable the default repos by renaming or moving the repo configuration files
*   If using installation media, mount it:  mkdir /dvd/ ; mount /dev/cdrom /dvd/
*   Create a new file:  # vi dvd.repo

[dvd-repo]
name=DVD-repo
baseurl=file:///dvd
enable=1
gpgcheck=1
gpgkey=file:///dvd/RPM-GPG-KEY-CentOS-6

The system should immediately recognize the newly created repo.  If you were using a network resource the baseurl would be http:// or ftp://.  Note that there are three slashes in a file URL:  two for the URL itself (file://), and one to indicate the root directory /dvd. 

As an alternative to listing the gpgkey by location, we could put it directly into the rpm database using rpm --import filename.  Not all repos will have a GPG Key, in this case set gpgcheck=0.  This turns off confirmation of repo and file integrity and can be a security risk.  It should only be done in a development environment.  After adding the repo, update the local cache files: yum makecache.  This will speed queries.

Use of yum itself is straightforward.  The most common invocation is yum -y install. 
The -y prevents yum from asking for permission at each step along the way.  To update software simply yum update.  Over time yum will accumulate old data in the form of caches, downloaded packages, etc. that need to be manually removed with yum clean all.  If you run out of space on /var, this should be one of your first steps toward resolution.

There are several separately installed packages that add useful functionality to yum. 

*   yum-plugin-security – provides the options --security, --cve, --bz, and
    --advisory so that yum can be instructed to only run security updates.

    *   man pages for the yum-plugins use short names, e.g. man yum-security
*   yum-cron – provides configuration for automated updates.
*   yum-updateonboot – will run yum update after boot.
*   yum-plugin-verify – adds the verify, verify-all, and verify-rpm commands, can be used like rpm -V.  Produces quite a bit of output and takes a long time to run.
*   yum-plugin-versionlock – will protect specified packages from being updated.

The primary configuration file for yum is /etc/yum.conf, some salient directives include:

*   gpgcheck / local_gpgcheck – these should both be set to 1, forcing yum to verify signatures on software before installing.
*   group_package_types – by default groupinstall will only install default and mandatory packages.  To install all in a group, set this to
    default, mandatory, optional.
*   keepcache – if set to 0, remove packages after install.
*   installonly_limit – the number of "install only" (versus upgrade) packages to have at one time.  The main "install only" package is the kernel, therefore this setting controls how many old kernels are retained.  Default is 5, recommended is 2, which is also the minimum.

rpm

As mentioned earlier, yum isn't an answer to everything; rpm is still sometimes needed.  Examples of common usages:

*   rpm -qf /usr/bin/yum – shows the package that installed the yum binary
*   rpm -qc yum – show yum's configuration files; useful when you don't know what to edit
*   rpm -qd yum – list all yum documentation
*   rpm -ql yum – list all files installed by yum
*   rpm -qlp /dvd/Packages/yum-3.4… – list all files in a package
*   rpm -q --scripts gnome-packagekit – show pre- and post-installation scripts
*   rpm -i or -U – install or upgrade

You will also need to verify the integrity of a system from time to time using rpm -Va.  This command scans all packages and checks them against the rpm database.  It can take quite a while to run. The output of this will look something like this:

SM5..UGT.  c /etc/plymouth/plymouthd.conf

Anything other than a series of dots in the first block means that something is different from the original installation.  The codes are:

*   S – file Size differs
*   M – Mode differs (includes permissions and file type)
*   5 – MD5 sum differs
*   D – Device major/minor number mismatch
*   L – symbolic Link path mismatch
*   U – User ownership differs
*   G – Group ownership differs
*   T – mTime differs

The c before the path means that this is a configuration file and can be safely ignored, as can xml files: rpm -Va |grep -v -e " c " | grep -v -e xml > file & will keep you from spending too much time looking at irrelevant results.  Note the spaces on either side of the "_c_".

Mode, User, or Group mismatches can be corrected by finding the package that controls the offending file with rpm -qf, then running rpm  --setperms, and/or rpm  --setguids on the package.  In the case of hash mismatches, indicated by a 5, the package should be reinstalled using rpm -Uh.

Installing Linux

EL6 can be installed from a DVD, USB, or network source.  The installation source is available at:

*   [https://www.centos.org/download/](https://www.centos.org/download/)  Get the DVD ISO, the 'Everything ISO' has all the sources, but defaults to a minimal installation.
*   [https://access.redhat.com/downloads/](https://access.redhat.com/downloads/)  Login required.  Get 'rhel-server…dvd'.
*   [https://getfedora.org/en/server/download/](https://getfedora.org/en/server/download/) Fedora versions 12-14 are roughly equivalent to EL6, but its use is not recommended as they reached end of life in 2008.
*   [https://www.scientificlinux.org/downloads/](https://www.scientificlinux.org/downloads/)
*   [http://www.oracle.com/technetwork/server-storage/linux/downloads/index.html](http://www.oracle.com/technetwork/server-storage/linux/downloads/index.html) Login required.

Be aware that later versions (EL7+ and Fedora 15+) represent major changes and have many features not addressed in this version of our book.  The introduction of systemd changes things quite a bit. 

After you've downloaded the source, you can simply burn it to a DVD.  To create a bootable USB image from a Linux machine, ensure that your USB device is unmounted then:
dd if=/path/to/boot.iso of=/dev/sdX bs=512k
where sdX is the path to the usb device. 

If you need to create a bootable USB from Windows or Mac, use the FedoraMediaWriter available at https://github.com/MartinBriza/MediaWriter/releases.  Methods for installation from network sources can vary wildly.  The official documentation should be consulted.

The initial boot menu has five options: Install or upgrade, Install with basic video, Rescue installed system, Boot from local drive, and Memory Test.

You can also press tab to break out of this menu and add options to the end of the command line.  Press enter to continue installing.  Options include:

*   dd – Add drivers from a URL.  If the installer detects essential hardware that it does not have a driver for, it will prompt you.
*   inst.ks=ftp://localserver/pub/ks.cfg – Use a kickstart script rather than answering all those questions. 
*   text – Force a text mode install.
*   rescue – run the rescue environment.
*   dracut options – More in the dracut.cmdline man page.
*   fips=1 – enable FIPS 140-2 compliance. 

On government systems the fips=1 option should always be added during installation.  While fips compliance can be enabled later, the procedure is much more involved.  Enabling fips after the fact can potentially break certificates and keys that were generated using less rigorous standards, as well as resulting in errors in common programs.  After installation, you can confirm that fips is enabled by viewing /proc/cmdline or with sysctl crypto.fips_enabled.

Both for practicality and for STIG compliance you should create partitions beyond the installer default of /, /boot, and swap.  Each of the following should have its own partition /tmp, /var, /var/log, /var/log/audit, /home.  Obvious, but sometimes overlooked, swap should be of file system type swap.

You will then be led through a straightforward installation.  You can configure hostname and IP address, root password, and partitioning information.  On the security side, you can encrypt the hard drive and set a boot loader password.  Encrypting the hard drive will require manual intervention on each boot.  The boot loader password is only needed to alter the boot sequence. These passwords and phrases should each be unique.

Note that the default install is often very minimal if you do not click on "Customize now" and add additional packages.  Note that on many of the tool sets, simply checking the category (such as Base System, Backup Client) will not actually select software for install – you will need to drill into the "Optional Packages" for each. 

Do not install anything you don't need.  Be particularly careful with server components (which you'll need to uninstall or secure later) and Desktop components (General Purpose Desktop includes, among other things, a music library manager).

After installation and reboot, you will be presented with a short menu sequence prompting you to accept the license, create a secondary user, set date and time, and enable kdump.  For security reasons, kdump must be disabled.  It is a kernel level debugging tool which will record kernel level memory (possibly including sensitive information) to a file in case of a crash.

kickstart

While you can use the installer for individual machines, if you are doing multiple installs it is much easier to pre-specify everything in a script.  This is done using kickstart.  Every installation will have a kickstart file which can be used to replicate the installation at /root/anaconda-ks.cfg.

You can also get a template kickstart file by installing the scap-security-guide package.  Among other things, this will place several kickstart templates in
/usr/share/scap-security-guide/kickstart/.  There will be one for STIG deployments and another for the US Government Common Baseline (usgcb).  These will run the oscap tool in remediation mode when complete and place the results in /root/. 

These files can be modified to meet your particular needs:

*   Uncomment an installation method, such as cdrom.  If you don't do this, it won't work.
*   Change rootpw – default is 'server'.  Generate a new hash using grub-crypt --sha-512
*   Change bootloader --password= – default is 'password'.
*   Adjust networking if desired – default is DHCP
*   Adjust partition sizes –   --size = is expressed in MB

    *   Best practice says to make /var/log/audit 1024 MB minimum
*   Adjust package installation for your environment

    *   Do not remove git, aide, or any scap or openscap packages

You can share the kickstart on a network, or place it in a locally available file.  Invoke the script by using the ks= argument on the installation command line.  For fully automated installation this can even be done using network boot.

After you have completed installation.

*   Accept the license terms.
*   Create a non-root user.
*   If prompted by firstboot, disable kdump.
*   Do the basic configuration as set out in Module 1.
*   On RHEL systems,

    *   register it with Red Hat so you have access to their repos.
    *   disable and mask rhnsd.service, this automatically queries Red Hat servers for actions such as update and is not appropriate for a secure system.
*   Update packages and kernel using yum.
*   Secure the system as outlined in the Security module.

VMware Tools

If you are using an EL6 install in a virtual machine running on VMware ESXi, you will want to install VMware Tools, which provides a better user experience, better drivers for virtualized hardware, and guest operating system visibility from VMware.  On EL7 and later versions an open source version of Tools is automatically installed.  On EL6, the process is a bit more involved:

First you must import the VMware GPG DSA & RSA keys:

# rpm --import https://packages.vmware.com/tools/keys/VMWARE-PACKAGING-GPG-DSA-KEY.pub

# rpm --import https://packages.vmware.com/tools/keys/VMWARE-PACKAGING-GPG-RSA-KEY.pub

Check that they installed using:  rpm -qa gpg-pub* | xargs rpm -qi | grep VMware

You will need to identify your exact version of ESXi, your EL distro and version, and hardware architecture.  With this information in hand, browse to the appropriate URL, beginning with

[https://packages.vmware.com/tools/esx/index.html](https://packages.vmware.com/tools/esx/index.html), copy the URL of the proper repo for use as baseurl later.

Next, create /etc/yum.repos.d/vmware.repo:

[vmware-tools]

name=VMware Tools

baseurl=https://packages.vmware.com/tools/esx/5.1/rhel6/x86_64

enabled=1

gpgcheck=1

Then yum install vmware-tools-esx*. 

Note: the packages will not list as available or show any info through yum, but will install correctly.

Module 15:
Remote File Systems

NFS

NFS is the Network File System, developed in 1984 by Sun.  The early versions of the protocol were stateless and connectionless, simply executing remote procedure calls over UDP.  With the advent of NFSv4 in the early 2000s we received a few security upgrades, including a mandate to run over TCP and the ability to integrate with Kerberos.  This material will deal exclusively with NFSv4.

Let’s walk through setting up an NFS server and exporting a file system.  After installing nfs-utils, we can start the service. 

# service nfs start

Starting NFS services:                                     [  OK  ]

Starting NFS quotas:                                       [  OK  ]

Starting NFS mountd:                                       [  OK  ]

Starting NFS daemon:                                       [  OK  ]

Starting RPC idmapd:                                       [  OK  ]

To make file systems available remotely, an administrator only needs to create the file /etc/exports and execute exportfs. 
Each line in /etc/exports represents an exported file system and will contain these fields:

[local FS to share] – /home, /svr/share, /var/pub

[hostname] – client, client.local, www.site.not

[network] – 192.168.0.0/24, 172.16.0.0/28 (note the slash notation)

[options]

rw – allow read and write access

sec= – define a list of allowable security flavors (sys:krb5:krb5i:krb5p)

sync – do not reply to NFS request until a write has occurred

fsid=0 – sets the “root” of the virtual file system in NFSv4

anonuid – set the system UID to be assigned to anonymous users

no_root_squash – do not map UID 0 requests to anonymous

This is a sample /etc/exports file from the man page:

/               master(rw) trusty(rw,no_root_squash)

/projects       proj*.local.domain(rw)

/usr            *.local.domain(ro) @trusted(rw)

/home/joe       pc001(rw,all_squash,anonuid=150,anongid=100)

/pub            *(ro,insecure,all_squash)

/srv/www        -sync,rw server @trusted @external(ro)

/foo            2001:db8:9:e54::/64(rw) 192.0.2.0/24(rw)

/build          buildhost[0-9].local.domain(rw)

Note the use of wildcards in the examples.  This is not a secure practice.  To demonstrate this, let’s consider a simple exports file:

# cat /etc/exports

/home *(rw,sync)

Here, the asterisk indicates that we are willing to share our /home directory with read/write permission with anyone who asks.  Let’s make a slightly more secure export, allowing a single host read/write access to  /test.

# cat /etc/exports

/test 192.168.1.162(rw,sync)

Once we’ve created our desired exports file, we next need to export it.  We can do this with exportfs.  See below:

# exportfs -va

exporting 192.168.1.162:/test

We can verify that we are successfully exporting /test by running the exportfs command with no options (nfs will need to be started before this command will return results).  This will display a list of currently exported filesystems.

With the export done, we must consider how clients will access our new share.  NFS uses 2 layers of permissions: those defined in the export options, and those defined in the metadata and extended ACLs of the files being accessed (NFSv4 is required for extended ACL support).  NFS determines permissions based on the account name and UID of the accessing user, and cannot grant access that a user would not otherwise have been granted locally. 

Of course, no amount of permissions will ever be sufficient if we cannot get through the firewall.  NFSv4 only requires a single TCP port for initial service connection: TCP 2049.  Let’s add a simple rule to iptables allowing NFS to be served on TCP 2049, but only to our partner server.

# iptables -I INPUT -s 192.168.1.162/32 -p tcp --dport 2049 -j ACCEPT

# iptables -L

Chain INPUT (policy ACCEPT)

target     prot opt source         destination

ACCEPT     tcp  --  192.168.1.162  anywhere            tcp dpt:nfs

ACCEPT     tcp  --  anywhere       server.example.local tcp dpt:http

<truncated>

Let’s also check to see that nfs is listening using ss:

ss -tlp | grep nfs

LISTEN     0      64               :::nfs                     :::*

LISTEN     0      64                *:nfs                      *:*

Now that the port is open, we need to perform a little housekeeping so that services like rpcbind will NOT try to serve NFS v2/3.  In /etc/sysconfig/nfs set the following option:

# Optional arguments passed to rpc.mountd. See rpc.mountd(8)

RPCMOUNTDOPTS="-N 2 -N 3"

We should be done with configuration on the server side (for the moment).  Let’s restart the nfs service: # service nfs restart

Note that these changes will cause certain services to become unavailable.  For example, the showmount command will no longer function, as it only works with older versions of the NFS protocol.

We’ll also need to make some configuration changes on our NFS clients if we want things to work smoothly.  EL6 ships with NFSv4 capable NFS clients installed (or, if installing from default repositories, the latest versions of the client will support it).  Configure the global NFS mount options in the /etc/nfsmount.conf file, by uncommenting the following:

Defaultvers=4

Nfsvers=4

Defaultproto=tcp

Proto=tcp

When this is done, we may attempt a mount.

# mount -t nfs 192.168.1.164:/test /mnt

# ls /mnt

1       directory  inode.example  newfile  pathfile

binary  file       link           outfile  source

Above, we first specified a mount type of nfs and succeeded in mounting the exported file system with the default of NFSv4.  We verified that we have mounted and listed the contents of the file system, but we haven’t tried to write to it.  Let’s try that now:

# ls /mnt

1       directory  inode.example  newfile  pathfile

binary  file       link           outfile  source

# touch /mnt/somefile

touch: cannot touch ‘/mnt/somefile’: Permission denied

The export from our NFS server granted us read and write but we don’t seem to have it.  From the client, running the mount command returns this:

# mount | grep /mnt

192.168.1.164:/test on /mnt type nfs4 (rw,relatime,vers=4.0,rsize=262144,wsize=262144,namlen=255,hard,proto=tcp,port=0,timeo=600,retrans=2,sec=sys,clientaddr=192.168.1.162,local_lock=none,addr=192.168.1.164)

Here, we have verified that we did mount with read and write permissions.  We know from our earlier work that the file system was exported with read and write permissions as well.  From the server, we examine the permissions on the exported file system with ls -ld:

# ls -ld /test

drwxr-xr-x. 4 root root 4096 Jul 25 15:35 /test

Note the last triplet: others do not have write access to this directory.  When we mounted the share, we were logged in locally as root, but we were not treated as such on the server.  Instead, we were squashed by the default root_squash option; that is, while we may be root on the client system, we were not allowed to be root on the host system.  root_squash transformed us into an unprivileged, anonymous user.  Best practice is to avoid no_root_squash if possible, as it will disable this behavior.

vsftpd, lftp

Use of FTP is generally not recommended, as it is unencrypted and passwords will be passed in plain-text.  But, there are times when it is the right solution, such as when providing an appropriately firewalled software repository for internal use, or when making large files available to the public.

The standard ftp server for EL6 is vsftpd, and it is not installed by default.  For a simple installation, you will want to add vsftpd to the init sequence with ckconfig vsftpd on.  The configuration file for the service is /etc/vsftpd/vsftpd.conf.  Some relevant options are:

*   anonymous_enable – set to NO unless needed
*   write_enable – set to NO unless needed
*   anon_upload_enable – default NO.  Also enforced by SElinux booleans
*   ftpd_banner – leave commented out instead use banner_file
*   banner_file – point to /etc/issue, put your banner there
*   listen_ipv6 – slightly deceptive, as this enables both IPv4 and 6
*   ssl_enable – a pain to configure and affected by the several flaws, use sftp instead
*   delay_failed_login – if allowing authenticated connections, set this to 10 or more.

Before starting the service, check permissions and SELinux context on /var/ftp/.  This is the default directory for anonymous users.  Anonymous users are logged in as user ftp.  To change the default directory, change the user ftp's home directory.  You will also need to open ports in your firewall to allow communication with the service.  For active FTP, you’ll need to allow inbound on TCP port 21, and outbound on TCP port 20.  For passive FTP, incoming on TCP port 21 is sufficient; however, outbound ports will be generated randomly in the ephemeral range.  This is a problem if your OUTPUT chain is configured with a default drop policy.  To fix this issue, you can add a line in /etc/sysconfig/iptables-config: IPTABLES_MODULES=”ip_conntrack_ftp”. 

This loads a connection tracking module that can be used to identify packets associated with FTP streams.

The usual ftp client for EL6 is lftp, which supports other protocols, including http.  The common syntax is lftp [user@]hostname.  Many commands (such as put and get) are retained from older ftp clients.  Others such as lls, have been replaced with the syntax !ls, where the ! invokes the local shell.  The one exception to this lcd which is the only way to change the local directory.

httpd, httpd.conf

Getting a basic web server running on EL6 is very easy.  First install the Apache webserver:  httpd.  If you wish to use authentication, httpd-tools is required.  httpd-manual will place the full html documentation for apache at http://localhost/manual. 

Place a file named index.html into /var/www/html,otherwise /etc/httpd/conf.d/welcome.conf will display). 

Firewall ports will need to be opened for http (80) and/or https (443).  The service can then be started with service httpd start.

The primary configuration file for Apache is /etc/httpd/conf/httpd.conf.  The options contained within it are called directives.  The "quick" reference guide to Apache directives is over 30 pages long, and configuration can be quite complex, but some relevant directives include:

*   Listen – This should have both an IP and port.
*   DocumentRoot – the base directory for service.
*   To prevent DoS attacks the following should be set:

    *   LimitRequestFieldSize   8190 – or less
    *   LimitRequestLine  8190 – or less
    *   LimitRequestBody   1 – or more
    *   LimitRequestFields   1 – or more
    *   KeepAliveTimeout   15 – or less
    *   KeepAlive   On
    *   Timeout   300 – or less
*   All <Directory/> entries should have AllowOverride   None

Configuration of secure web services using https and authentication varies wildly based on site and application specifics, and is too broad a topic to address here.

curl, wget, lynx

There are times when you will need to get content from a webserver, but only have a command line.  There a few tools that you can use to solve this problem.  curl and wget both work from a simple command line and can be encapsulated in scripts.  Both support FTP, HTTP, and HTTPS protocols as well as cookies and POST requests, but there are some differences:

*   curl

    *   output can be piped, basically acts like cat for networks
    *   will not recurse a website
    *   supports many protocols including SFTP, SCP, TFTP, POP3, IMAP, and LDAP
    *   automatic decompression HTTP deflate/gzip
*   wget

    *   output goes into a file or files
    *   can recurse a website, will create a directory structure matching that of the original
    *   will automatically resume if a connection is interrupted

Both curl and wget have their place, but to actually browse the web, you need something that understands html.  For that you need lynx.  Navigation in lynx is simple:

*   g – go to URL
*   + / - or space / shift-space – go down or up
*   up / down – move between hyperlinks
*   right – select link
*   left – go back
*   q – quit

While lynx doesn't support all the features of a graphical browser, it can be used in a pinch.  It also is a good way to verify the accessibility features of a website.

Module 16:
Remote Access

As a general rule, administrators no longer sit in front of the servers they are running.  Instead we use remote access protocols.  We no longer move files using disks or tapes, rather we use the network.  We will explore how to access machines from both the server and client-side in this module.

vnc

If your destination server is in graphical mode, you can access the full GUI using vnc (Virtual Network Computing).  First ensure tigervnc and tigervnc-server are installed, and that the service is allowed through the firewall.  How this is done will depend on how many users are configured for vnc access.  The vnc server will need ports open in a range, with separate ports for each user (or display).  We will assume vnc configuration for two users:

# iptables -I INPUT 3 -m state --state NEW -m multiport -p tcp --dports 5800,5900,6000 -j ACCEPT

# iptables -I INPUT 3 -m state --state NEW -m multiport -p tcp --dports 5801,5901,6001 -j ACCEPT

# iptables -I INPUT 3 -m state --state NEW -m multiport -p tcp --dports 5802,5902,6002 -j ACCEPT

# iptables -L

Chain INPUT (policy DROP)

target     prot opt source               destination

ACCEPT     tcp  --  anywhere             anywhere           state NEW multiport dports 5802,5902,6002

ACCEPT     tcp  --  anywhere             anywhere            state NEW multiport dports 5801,5901,6001

ACCEPT     tcp  --  anywhere             anywhere            state NEW multiport dports 5800,vnc-server,x11

Note here that the base ports required for vnc are TCP 5800, 5900, and 6000.  Every user, including the initial single user, will need a port incrementally higher than the last; in this case, TCP 5801, 5901, 6001 for the first user, and one number higher on each for the second user.  The last digit or two will correspond to the display number for the vnc service (more in a moment).

Each user will need a vnc-specific password.  The user themselves should set this directly as the vncpasswd command creates a unique password hash stored in ~/.vnc/passwd.

We can do this on behalf of the user by assuming their identity with su. 

# su - user ; vncpasswd

To start the service manually, use the vncserver utility.  This is a bundled perl script designed to simplify the process of starting vnc sessions.  It will take the format of:

vncserver :number

For example, vncserver :2 will start display session 2.  Please note, however, that this command will create session support files in the home directory of the invoking user.  This is not always the desired behavior, and can lead to conflicts. 

Further, any sessions started with the vncserver command will not persist beyond a reboot, and may not shut down cleanly. 

A better way, and one that will make sessions available at boot time, is to make changes to /etc/sysconfig/vncservers, as below:

VNCSERVERS="1:vncuser 2:vncuser2 "

VNCSERVERARGS[1]="-geometry 1920x1280 -nolisten tcp"

VNCSERVERARGS[2]="-geometry 1920x1280 -nolisten tcp"

This file will be read when the service is started or restarted.  We can start the service with service vncserver start. To make this configuration persistent, we need to add vncserver to the appropriate runlevels with chkconfig vncserver on.

You can now open a session to the server using
vncviewer user@remotehost  remotehost:number 

You can also access the destination from other operating systems using a third party viewer.

ssh, ssh-keygen, ssh-copy-id

ssh is a replacement for insecure shell protocols such as telnet, rlogin, and rsh, which should no longer be used under any circumstances.  It allows the secure passing of credentials and an encrypted channel between machines.  It also provides the underlying protocol for secure copy protocol (scp) and secure FTP (sftp).  Both client and server must be installed and configured on a secure system.  Installation can be confirmed with yum list installed *ssh*.

Improperly configured ssh can be a very large security hole.  To ensure that ssh is configured correctly:

In /etc/ssh/sshd_config

*   Uncomment and/or change:

Protocol 2 ## and only 2

PermitEmptyPasswords no

PermitUserEnvironment no

GSSAPIAuthentication no

ClientAliveInterval 600

ClientAliveCountMax 0

IgnoreRhosts yes

PrintLastLog yes

PermitRootLogin no

IgnoreUserKnownHosts yes

KerberosAuthentication no

StrictModes yes

Compression delayed (or no)

*   Add:

HostbasedAuthentication no

Ciphers aes128-ctr,aes192-ctr,aes256-ctr

MACs hmac-sha2-256,hmac-sha2-512

banner=/etc/issue  ## insert your banner in /etc/issue

RhostsRSAAuthentication yes

*   Leave at default:

UsePrivilegeSeparation sandbox

X11Fowarding yes

In /etc/bashrc add a line: TMOUT=600.  Then, find and remove any file with the name shost, rhost or *hosts.equiv.  These files could potentially allow users from "trusted hosts" direct access with no additional verification. 

Next check permissions on the host keys:

chmod 0644 /etc/ssh/*key.pub

chmod 0600 /etc/ssh/ssh_host*key  

Finally, add or update the following line in /etc/audit/rules.d/audit.rules:
-a always,exit -F path=/usr/libexec/openssh/ssh-keysign -F perm=x -F auid>=1000 -F auid!=4294967295 -k privileged-ssh

Basic use of ssh is simple: ssh user@remotehost.  You can also perform fully certificate-based logins.  This adds an additional layer of security, and has the advantage of allowing the use of different (even random) passwords on each machine, without having to track each one individually.

To do this correctly the source user and destination user must exist on both machines – and have the same UID.  If the UID is used by another user on the destination machine, you will log in as that user and have access to that users files!  To avoid this, it is best practice to create users in a higher, reserved UID space (say 3000 and above) specifically for this purpose.

To use certificate-based ssh, you must first create a key:  ssh-keygen.  Follow the prompts. 

Then copy the key to the remote server: 
ssh-copy-id -i /path/to/key user@remotehost 

You can now log in using the key, rather than the password:
ssh -i /path/to/key user@remotehost 

scp, sftp

As mentioned, you can also use ssh framework to transfer files using scp.  This allows secure and simple transfer between hosts, without requiring the configuration of a separate server.  You can even use certificates.  The basic invocation is simple:

scp -i /path/to/key localfile user@remotehost:/path/remotefile

It will accept wildcards such as /path/dir/*.tgz, and can recurse entire directory trees (-r).

If you need to do more than simply move a single file or directory you can use sftp.  The sftp-server is invoked as a subsystem of sshd.  By default it is on and configured by the following line from sshd_config: Subsystem   sftp    /usr/libexec/openssh/sftp-server.  This allows system-wide sftp rights (controlled by standard permissions, of course). 

To restrict users (in this example, the group sftp-u) only use sftp, preventing ssh, replace the Subsystem line in sshd_config with:

Subsystem       sftp    internal-sftp

and append:

Match Group sftp-u

ForceCommand internal-sftp

To restrict them to a single directory add
ChrootDirectory /sftp/%u.
The %u will be replaced with the username upon login. 

Then create a directory for that user:  /sftp/username/home. 
chown the home directory only (not the path above it) to username:sftp-u.

Restart sshd after making changes.

Module 17:
Kernel Modules and Parameters

An operating system kernel forms the core of the OS, and is responsible for the direct access and manipulation of a system’s hardware.  Typically, the kernel will, by design, be small and light; it will have capabilities required to boot a system and operate things like memory and processors, and a minimal set of tools for dealing with storage or networking.

When an operating system requires greater capabilities (wifi networking, dealing with special types of storage, interacting with graphics cards, etc.), these will be provided by drivers – or, in the Linux world, kernel modules.

Kernel modules are chunks of code that can be added to a kernel to extend its capability set.  These come in two basic types:

*   Static modules must be compiled into the kernel to operate.  This requires a kernel recompile and a system reboot.  Further, it leads to a larger kernel memory footprint and an increase in the amount of time required to bring a system up.  Static modules are usually chosen in situations where a system cannot fully boot without the capabilities offered in the module.
*   Dynamic modules, by contrast, may be loaded or unloaded as needed.  In this way, we can keep the kernel small and lean, resulting in faster boot times and more efficient use of system resources.  In the most general sense, dynamic modules will be preferable to static modules. 

To see a list of kernel modules currently available on our system (and a brief list of other modules that depend on them), we can use the lsmod command.

# lsmod

Module                  Size  Used by

autofs4                21076  3

bnx2fc                 80024  0

cnic                   47474  1 bnx2fc

uio                     7822  1 cnic

fcoe                   19570  0

libfcoe                47527  2 bnx2fc,fcoe

libfc                  96173  3 bnx2fc,fcoe,libfcoe

8021q                  16617  0

<truncated>

While interesting, this list doesn’t give us much information.  In fact, it’s not much more than a formatted list of the contents of the /proc/modules virtual file.

# cat /proc/modules

autofs4 21076 3 - Live 0xfa475000

bnx2fc 80024 0 - Live 0xfa450000

cnic 47474 1 bnx2fc, Live 0xfa421000

uio 7822 1 cnic, Live 0xfa40a000

fcoe 19570 0 - Live 0xfa3fa000

libfcoe 47527 2 bnx2fc,fcoe, Live 0xfa3db000

libfc 96173 3 bnx2fc,fcoe,libfcoe, Live 0xfa3a9000

8021q 16617 0 - Live 0xfa380000

<truncated>

Accordingly, the best use of lsmod is in determining the existence or nonexistence of a particular module.  We can get more specific information about these modules by using the modinfo command.

# modinfo bnx2fc

filename:       /lib/modules/2.6.32-696.el6.i686/kernel/drivers/scsi/bnx2fc/bnx2fc.ko

version:        2.10.3

license:        GPL

description:    QLogic FCoE Driver

author:         Bhanu Prakash Gollapudi <bprakash@broadcom.com>

srcversion:     A16D9357AE40732F3FB574A

depends:        libfcoe,libfc,scsi_transport_fc,cnic

vermagic:       2.6.32-696.el6.i686 SMP mod_unload modversions 686

parm:           debug_logging:Option to enable extended logging,

Default is 0 - no logging.

0x01 - SCSI cmd error, cleanup.

0x02 - Session setup, cleanup, etc.

0x04 - lport events, link, mtu, etc.

0x08 - ELS logs.

0x10 - fcoe L2 fame related logs.

0xff - LOG all messages. (int)

parm:           log_fka: Print message to kernel log when fcoe is initiating a FIP keep alive when debug logging is enabled. (uint)

The bolded output above shows that the bnx2fc kernel module has associated parameters.  Parameters are configurable values that modify the behavior of kernel modules.  To alter kernel module parameters, we would use either the sysctl or modprobe commands.  As modprobe is capable of handling multiple module-related tasks (and in a safer, more controlled fashion than some older commands), it makes sense to focus our examples on its usage.  Below, we will attempt to use modprobe to alter the debug_logging parameter of the bnx2fc module, setting its value to 0x01.

# modprobe bnx2fc debug_logging=0x01

#

The response to this command seems to indicate success; but did we really change anything?  To check, we can look in /sys/module/bnx2fc/parameters/. 

# ls /sys/module/bnx2fc/parameters

debug_logging  log_fka

# cat debug_logging

0

This tells us that the current value for the debug_logging parameter is still 0.  If that’s true, why did the earlier command seem to succeed?

The answer lies in understanding that kernel module parameters cannot be altered while the module is in use.  When we ran the command modprobe bnx2fc debug_logging=0x01, we weren’t instructing modprobe to alter that parameter on a running module.  Instead, we were asking modprobe to load the module with that value.  When it ran, modprobe simply took note of the fact that the bnx2fc module was already loaded and exited with a return code of 0.

If we truly wish to alter this parameter, we must first unload the module.  Before we attempt this, we should first check to see if any other modules are dependent on it.

# lsmod | grep bnx2fc

bnx2fc                 80024  0

cnic                   47474  1 bnx2fc

libfcoe                47527  2 bnx2fc,fcoe

libfc                  96173  3 bnx2fc,fcoe,libfcoe

scsi_transport_fc      43160  3 bnx2fc,fcoe,libfc

The above output tells us that, while bnx2fc depends on several other modules, it doesn’t seem that any other modules depend on it.  We’ll try using modprobe to unload it, but first, let’s trace some of the dependency tree:

# modinfo -F depends bnx2fc

libfcoe,libfc,scsi_transport_fc,cnic

# modinfo -F depends cnic

uio,ipv6

# modinfo -F depends uio

# lsmod | grep ^ipv6

ipv6                  272327  38 cnic,ip6t_REJECT,nf_conntrack_ipv6,nf_defrag_ipv6,ib_ipoib,ib_addr

Above, we’ve selected one of the dependencies that bnxfc2 relies on, cnic.  We then listed the dependencies for cnic, and selected uio for further tracing.  Inspection shows that uio has no further dependencies.  Finally, we used lsmod to determine that the ipv6 module is a dependency for 38 other kernel modules.

We’ve traced these dependencies to illustrate a behavior of modprobe.  When we instruct modprobe to remove a module:

*   modprobe will not remove a module that is in use by a device or process
*   modprobe will not remove a module that is used as a dependency for another active module
*   modprobe will intelligently unload a module upon which it was dependent, if that module is no longer be needed

The last bullet is best understood by observation.  Let’s unload the bnx2fc module now, and watch what happens:

# modprobe -r -v bnx2fc

rmmod /lib/modules/2.6.32-696.el6.i686/kernel/drivers/scsi/bnx2fc/bnx2fc.ko

rmmod /lib/modules/2.6.32-696.el6.i686/kernel/drivers/net/cnic.ko

rmmod /lib/modules/2.6.32-696.el6.i686/kernel/drivers/uio/uio.ko

Above, we asked modprobe to unload bnx2fc.  This was done, but the cnic and uio modules were also removed.  Because they were no longer required.  The only module using cnic and uio as a dependency was bnx2fc; no other device, process, or module required them.  When bnx2fc was unloaded, cnic and uio no longer served any purpose, and were therefore dismissed.  The ipv6 module was NOT unloaded, because it was still needed for other purposes.

Now that the bnx2fc module has been removed, we can launch it again with desired parameters. 

# modprobe bnx2fc debug_logging=0x01

# cat /sys/module/bnx2fc/parameters/debug_logging

1

The command succeeded, and we have verified the new parameter setting. 

(Quick Note:  If you’re wondering why a value of “0x01” is being reported as “1” in our output, it’s because this notation, “0x”, simply indicates that the following value will be described in hexadecimal format.  01 in hex is equal to 1 in decimal.)

At this point, we have succeeded in manually loading and unloading kernel modules, and in altering the parameters of a manually loaded module at load time.  These changes, however, will not be persistent.  If the module is unloaded and loaded again, either manually or by any other process (during boot for example), it will be initiated with the default values for all parameters.

To make our changes persistent, we will need to modify or create configuration files.  Several options exist for accomplishing this task; we will again endorse modprobe as the best tool for this task.

To begin, we’ll relocate to the /etc/modprobe.d/ directory.  Any files placed in this directory will be referenced by modprobe.  We can create files here with any we like, so long as it ends with .conf. The file name is not important but the internal structure and values are.

We’re altering the bnx2fc module, so it makes sense to name our configuration file accordingly:

# cd /etc/modprobe.d

# ls

blacklist.conf        dist.conf      libcxgb4.conf  openfwwf.conf

blacklist-visor.conf  dist-oss.conf  libmlx4.conf

dist-alsa.conf        libcxgb3.conf  mlx4.conf

# echo "options bnx2fc debug_logging=0x02" > bnx2fc.conf

# ls

blacklist.conf        dist-alsa.conf  libcxgb3.conf  mlx4.conf

blacklist-visor.conf  dist.conf       libcxgb4.conf  openfwwf.conf

bnx2fc.conf           dist-oss.conf   libmlx4.conf

# cat bnx2fc.conf

options bnx2fc debug_logging=0x02

Above, we created the required configuration file using the line format of:

options module_name  parameter=value

When we unload and reload our module, we should see the value of the debug_logging parameter change to “2” as described in our configuration file.  Let’s try it out:

# modprobe -r bnx2fc

# modprobe -v bnx2fc

insmod /lib/modules/2.6.32-696.el6.i686/kernel/drivers/uio/uio.ko

insmod /lib/modules/2.6.32-696.el6.i686/kernel/drivers/net/cnic.ko

insmod /lib/modules/2.6.32-696.el6.i686/kernel/drivers/scsi/bnx2fc/bnx2fc.ko debug_logging=0x02

# cat /sys/module/bnx2fc/parameters/debug_logging

2

Blacklisting

In some situations, we may wish to prevent kernel modules from loading.  We might wish to prevent unstable behavior with a module, or avoid driver conflicts.  On high security systems, we may wish to prevent USB support modules from loading when a portable drive is plugged in.  While it is possible to entirely remove some modules from a system, we may prefer a less drastic option: blacklisting.

Blacklisting allows us to prohibit loading of kernel modules that exist on our system.  We can create a file to disallow a specific module using the same process we used to persistently set module parameters:

# pwd

/etc/modprobe.d

# echo "blacklist bnx2fc" > blacklist_bnx2fc.conf

# ls

blacklist_bnx2fc.conf  bnx2fc.conf     dist-oss.conf  libmlx4.conf

blacklist.conf         dist-alsa.conf  libcxgb3.conf  mlx4.conf

blacklist-visor.conf   dist.conf       libcxgb4.conf  openfwwf.conf

# cat blacklist_bnx2fc.conf

blacklist bnx2fc

This will prevent any automatic loading of the bnx2fc module.  It will not, however, prevent an administrator from manually load the module, or prevent the module from being loaded as a dependency for another non-blacklisted module.  To completely block this module from being loaded, we would need to add another line to our configuration file:

# echo "install bnx2fc /bin/true" >> blacklist_bnx2fc.conf

# cat blacklist_bnx2fc.conf

blacklist bnx2fc

install bnx2fc /bin/true

The effect of the highlighted line above is to essentially redirect any attempt to load the bnx2fc module to /bin/true, which will simply exit with code 0.  In other words, it will succeed in doing nothing.  You could also use /bin/false, which will do nothing, unsuccessfully.

Kernel Parameters

To this point, we have been discussing kernel module parameters.  There are also some parameters of the kernel itself that are exposed to direct manipulation.  We can get a list of these using the sysctl command:

# sysctl -a

kernel.sched_child_runs_first = 0

kernel.sched_min_granularity_ns = 1000000

kernel.sched_latency_ns = 5000000

kernel.sched_wakeup_granularity_ns = 1000000

kernel.sched_tunable_scaling = 1

kernel.sched_features = 7279

kernel.sched_migration_cost = 500000

kernel.sched_nr_migrate = 32

kernel.sched_time_avg = 1000

kernel.sched_shares_window = 10000000

kernel.timer_migration = 1

kernel.sched_rt_period_us = 1000000

kernel.sched_rt_runtime_us = 950000

kernel.sched_compat_yield = 0

kernel.sched_rr_timeslice_ms = 100

kernel.sched_autogroup_enabled = 0

kernel.sched_cfs_bandwidth_slice_us = 5000

kernel.panic = 0

<truncated>

We can alter these in realtime with the sysctl -w command (something like this: /sbin/sysctl -w net.ipv4.ip_forward = 0) , and we can alter them persistently by adding lines to the sysctl.conf file, in the following form.

# Controls IP packet forwarding

net.ipv4.ip_forward = 0

# Controls source route verification

net.ipv4.conf.default.rp_filter = 1

# Do not accept source routing

net.ipv4.conf.default.accept_source_route = 0

Changing or adding lines in the above file will alter the value for the specified parameter when next it is loaded.

Altering these parameters without full knowledge of the effects that will result is highly inadvisable.  Consequently, we have limited discussion of these processes to the cursory exploration above.

Module 18:
Disaster Recovery

dump, xfsdump, dd

There are many ways in EL6 to backup data.  Traditionally one of the most common toolsets for doing this was with the dump and restore commands.  These have been part of the system administrator's toolkit since 1975.  Today, dump is deprecated.  It is no longer installed by default, and does not support file systems beyond ext4.  There is a newer version, xfsdump (and xfsrestore), but even these should not typically be used on a live system.  The problem is that dump and xfsdump open a block device (disk) that is already mounted, ignoring the file system locks and unaware of write caches.  It can therefore get bad cached data.  Restoring a corrupted dump can destroy the entire file system's integrity.  If you really want to use dump, unmount the file system and remount it read only (or leave it unmounted entirely).  To quote Linus:
"Dump may work fine for you a thousand times. But it _will_ fail under the right circumstances. And there is nothing you can do about it." – Linus Torvalds

The same general stricture applies when using the copy utility dd on partitions or drives.  It can be used to perform a full backup of a device using
dd if=/dev/source of=/dev/dest conv=noerr. 

The noerr option tells dd to press on even if it has a read error.  Note that using this invocation dd will perform a byte-wise copy, wiping all data on the destination and copying everything (unlinked files and all) from the source.  This can also be used to copy a partition to a file (of=/path/file.bak).

There are many other uses of dd including:

*   converting optical media to iso image

    *   num=$(isosize -d 2048 /dev/cdrom) – set variable $num to the cd's block count
        dd if=/dev/cdrom of=some.img bs=2048 count=$num
*   creating a new file 

    *   dd of=/new/file – type at the command line, CTL-d when done.
*   repairing master boot records

    *   dd if=/dev/good/drive of=mbr.img bs=446 count=1 – copy boot code
    *   dd if=mbr.img of=/dev/bad/drive bs=446 count=1 – restore to bad drive

        *   bs=446 only copies the boot code
        *   bs=512 copies boot code and partition table
*   wiping drives

    *   dd if=/dev/zero of=/dev/sda bs=32M – zero sda with very large blocks
    *   shred is better for this, though it needs a special invocation for xfs files:

        *   shred -n 20 -fuz /xfs/file

tar, cpio

*   While dd and xfsdump can potentially mangle a backup of a mounted file system, tar will not.  It may copy a file to an archive while that file is being modified, in which case it may get a bad copy of that file.  But it will not break the underlying file system when restored.  Commonly used invocations for tar include: 
*   tar -czpf  arc.tar /etc/*.conf – where arc.tar is the archive and  /etc/*.conf is being archived

    *   -c – create archive
    *   -z – zip compress the archive
    *   -p – preserve permissions (happens for root by default)
    *   -f – archive filename follows, must be the last option
*   tar -tvf arc.tar

    *   -t – list contents of archive
    *   -v – verbosely
*   tar -xf arc.tar -C /alt/path

    *   -x – extract, modern tar will autodetect the compression type
    *   -C – change directory to /alt/path (otherwise tar will extract to the original path)
*   tar -cvf arc.tar $(find /etc/ -name f*.conf) – use the output of find as the list of files to archive

Individual files can be extracted by path as recorded by tar, wildcards acceptable.  Other useful options:

*   -d – find differences between archive and file system
*   -r – append files to archive
*   -u – update, append newer files
*   -l – store hard links as links
*   --dereference, --hard-dereference – store symlinks and hard links as full files
*   --acls – preserve extended acls, use when creating and extracting
*   --selinux – preserve SELinux context, use when creating and extracting
*   --xattrs – preserve both SELinux and acls attributes, use when creating and extracting

About the time tar was developed, another tool also came into availability: cpio.  It does almost exactly the same thing as tar, just in a different ways.  While both were included in the initial POSIX standard, cpio was dropped in 2001 because it had file size limitations.  Without standardization, differing versions went their own ways.  The defenders of cpio say it has some advantages:  it can take the input of a command, such as find, as a pipe, and it can store links either as links, or as separate copies of the referenced file.  It really isn't needed any more, but is still included in most distributions.

rsync

Everything discussed up to this point is for local copy and archive.  Though it can be used for local copy, rsync allows copy and archive between machines.  It is content aware, and will only transfer the differences between file sets and can compress files for bandwidth savings.  It can be used either as a stand-alone command to transfer between two machines; or it can be configured as a service, allowing multiple clients to synchronize files to a centralized server. 

In stand-alone mode rsync uses remote shell protocols such as ssh to perform the transfer.  Verify that you can ssh from the source to the destination machines before using rsync.  The basic format of the rsync command is:

rsync -av  /source/dir/  username@target.server:/dest/directory/

This will archive verbosely the contents of /source/dir/ to /dest/directory on target.server using usernames's credentials. 

If you omit the trailing / on the source, it will create the final directory name at the destination, e.g. /dest/directory/dir/.

To reverse the process, simply flip source and destination.  A source with no destination will list the files instead of copying.

Common switches for rsync include:

*   -a – archive, equivalent to -rlptgoD:  recurse, copy links; save permissions, timestamps, group, and owner; also preserve Device and special files.
*   -v – verbose
*   -z – compress (during transit, it will decompress at the destination)
*   -h – present human readable output
*   -e – use specified transport, such as "ssh -i /path/key"
*   -x – do not exit this file system
*   -X – preserve extended attributes
*   -H – preserve hardlinks
*   -A – preserve ACLs
*   -S – squeeze sparse files (those with long zero blocks)
*   -L – turn links into files
*   --delete – remove files not at the source, default is to preserve them at the destination
*   --remove-source-files – delete source upon success, useful for temporary tarballs
*   --include / --exclude / --filter – allows detailed specification of files

    *   e.g.rsync -av --exclude "*log*"  /var  remote.server/backup
    *   Filters can get quite involved, consult FILTER RULES in the man page.

To set up certificate based authentication add the following lines to ~/.ssh/config:
Host target.server
User username
IdentityFile /path/key

ReaR

ReaR (Relax and Recover) is a lightweight disaster recovery program capable either of standalone backup and recovery or as an adjunct recovery system for third-party backups.  At its most simple you create a backup server and backup to it.  In case of disaster, you make a copy of a boot image created for the failed computer, boot from it, and follow the menus.  It can generate .iso, USB, or PXE boot images.

To build the server you must install rear on both the clients and the server.  To create an iso based recovery disk, you will also need: genisoimage syslinux on the server. 

There are multiple transport methods available for ReaR backup and recovery. The most commonly used are rsync and nfs. 

For rsync to work, you will need to first establish ssh trust from the client to the target.  If you plan on running the backups manually, you can protect the private key with a passphrase.  To avoid having to enter the passphrase multiple times, you can load it into your current bash session:  eval $(ssh-agent); ssh-add /path/to/key 

If you are going to run the backup through cron, you will need to use a certificate with no passphrase.  In this case you should create a certificate just for backups and nothing else, adding a separate entry set (Host, User, IdentityFile) for the backup server.  If using rsync for recovery, you will be prompted several times for the root password of the backup server. 

The client is configured in /etc/rear/local.conf as follows:
OUTPUT_URL=rsync://servername/storage
BACKUP=RSYNC
BACKUP_URL=rsync://servername/storage
BACKUP_PROG_EXCLUDE=("${BACKUP_PROG_EXCLUDE[@]}" '/media' '/var/tmp' '/var/crash')

The user running the backup should have read permissions for the full system, and have full (rwx) permissions on the destination folder.  To initiate a backup run rear mkbackup, the switch -v will provide more feedback if desired.  The first backup may take some time, but because rsync only copies differences, later updates to the backup should run faster.  You may need to rm -Rf /tmp/rear.* afterwards.  To only make a backup use mkbackuponly, mkrescue only creates a rescue disk.

Additional configuration can be found at /usr/share/rear/conf/default.conf. 

To move a rescue disk to a VMware ESXi host for recovery, you can use  scp /path/XX/rear-XX.iso root@esxi:/vmfs/volumes/datastore/rear-XX.iso

The setup for ReaR over nfs is a little more involved on the server side.  It simplifies client configuration, as it doesn't require registering ssh certificates on a per client basis.  But it involves some level of insecurity, as there will be no authentication or encryption of the backup channel.  It also may not be as fast as rsync.  If you use nfs, it is strongly recommended that it be behind a firewall (preferably on an isolated VLAN), and that nfs is started only when needed.

To build the nfs server: install nfs, allow the following services through the firewall:  nfs, mountd, rpc-bind. It is best that these be placed in a separate, restricted zone.  Then create a directory (say /storage) with permissions of 777,  and add the following line to /etc/exports:

/storage   (fsid=0,rw,sync,no_root_squash,no_subtree_check,crossmnt)

On the client you will need to set these lines:

OUTPUT_URL=nfs://192.168.56.1/storage

BACKUP=NETFS

BACKUP_URL=nfs://192.168.56.1/storage

Module 19:
Security

We've addressed much of the implementation of the STIG and security best practices in the appropriate modules, and much can be accomplished using oscap and ansible as shown below, but some relevant points to keep in mind include:

*   Password protect the BIOS if possible
*   Disable alternate boot methods such as cdrom and USB
*   Use LUKS encryption whenever practical
*   If you don't know that you'll need it, don't install it.
*   If you don't need graphics all the time, set the default run level to 3 (multi-user)

    *   For the most part a server should not have graphics installed.
*   Disable, mask and uninstall services, sockets, groups, and packages if they are unneeded.
*   Consider restricting login hours using the pam_time module:

    *   In /etc/pam.d/login add account     required     pam_time.so
    *   Create rules in /etc/security/time.conf
*   Always login as an unprivileged user and use su or sudo
*   Force read-only for removable media

    *   create a file /etc/udev/rules.d/80-ro-media.rules add the following
    *   SUBSYSTEM=="block",ATTRS{removable}=="1",RUN{program}="/sbin/blockdev --setro %N"
*   If remote access is required, consider using an IPsec VPN tunnel using libreswan.

Additionally, you should reference: [https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Security_Guide/index.html](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Security_Guide/index.html)

Remove any non-essential software.  If you are concerned about dependencies, add groupremove_leaf_only=1 to the main section of yum.conf. This will prevent the removal of packages which others are dependent on.  If you want a list of software without parent dependencies: package-cleanup –leaves --all.

Groups to consider removing,

*   Desktop / General Purpose Desktop
*   Directory Client – CIFS, kde, samba, and some print utilities are dependent
*   Electronic Lab – contains x11 fonts
*   FCoE Storage Client
*   Fonts
*   Graphical Administration Tools – leave if you need VMware-tools
*   Graphics Creation Tools
*   Input Methods – for international language support
*   Internet Applications – mail and chat clients
*   Internet Browser
*   Java Platform
*   KDE Desktop
*   Legacy UNIX compatibility – tcp wrappers, disk quota is a dependency
*   Legacy X Window System compatibility
*   MySQL Database client
*   MySQL Database server
*   NFS file server
*   Network file system client
*   Networking Tools – some useful monitoring bits, but potentially insecure
*   Office Suite and Productivity
*   Performance Tools
*   Print Server / Printing client
*   Remote Desktop Clients
*   Scientific support
*   Storage Availability Tools – SAN multipath mapper
*   Web Server
*   Web Servlet Engine
*   X Window System
*   iSCSI Storage Client
*   Language Support Packages – these are listed in the format Arabic Support [ab], and will autocomplete as Arabic\ Support\ \[ab\], but must be named in the format arabic-support to be successfully removed by yum.

Individual programs to consider removing:

*   alsa-utils – command line for sound
*   autofs – automatically mounts file systems
*   avahi-daemon – provides Zeroconf networking
*   bind* – DNS server
*   bluetooth – nobody needs this on a server
*   cdparanoia, vorbis-tools, brasero, icedax – media stuff
*   certmonger – keeps CA certificates enrolled
*   colord – manages color profiles for graphics
*   cups / lpd / hplip / foomatic / redhat-lsb-printing – provides printer support
*   dhcp – the dhcp server
*   dovecot – imap & pop3 server
*   firstboot – not needed after install
*   fprintd – fingerprint scanner support
*   gpm – mouse for console
*   hidd – bluetooth mouse and keyboard support
*   httpd – web server
*   irqbalance – balances between processors, not needed on single socket machines
*   iscsi-*– iscsi protocol support
*   krb5-appl-clients – Kerberos versions of ftp, rcp, rlogin, rsh and telnet.
*   libvirtd – virtualization daemon
*   mcstrans – interprets SELinux categories to user defined labels
*   mdmonitor – software raid
*   microcode_ctl – transforms and deploys CPU microcode
*   ModemManager – for wireless modems
*   net-snmp – SNMP server
*   nfs, nfslock, rpcgssd, rpcbind, rpc.mountd, rpcidmapd, rpcsvccgssd, netfs – NFS
*   NetworkManager – as addressed in the networking module
*   oddjob – provides privileged access to unprivileged processes, never use
*   openldap-servers – for authentication
*   portreserve – pre-allocated ports for services
*   psacct – process stats and info provides ac, sa, accton, and lastcomm
*   rhnsd – Red Hat proprietary update agent
*   samba – file sharing
*   setroubleshoot – warns users of SELinux violations
*   squid – web proxy
*   vsftpd – FTP server
*   wireless-tools – not on a server
*   xinetd, telnet, rsh, rlogin, ypbind – defunct network protocols, never use

aide, aide.conf

After configuration of a new system, you should install aide, the advanced intrusion detection environment.  aide detects file tampering by scanning all files and folders while in a known good state, producing a baseline from that scan, and comparing that baseline to the current state.

The configuration file is /etc/aide.conf.  aide uses multiple means to compare files, including a default set of hashes which are not present on a fips compliant system.  Before use, these hashes should be disabled in aide.conf.  These changes should be followed exactly to get aide to work on a fips system.

Add:

N     =       p+i+n+u+g+s+m+c+acl+selinux+xattrs+sha512

Edit:

ALLXTRAHASHES = sha512
EVERYTHING = N
NORMAL = N
LSPP = N
DATAONLY =  p+n+u+g+s+acl+selinux+xattrs+sha512

Folders and files which are expected to be changed in the normal course of business should be excluded using one of these directives:
! /dirname prevents scanning of the directory entirely, or
/dirname CONTENT_EX, excludes content, but monitors permissions, SELinux context, etc.

This should be done if you encounter too many false positives using the default aide.conf.  After configuration changes, the integrity of the configuration file should be checked with
aide -D.  Remotely mounted devices should be excluded from local scan, instead they should be scanned by the hosting device. 

Before using aide, you must create an initial database with aide -i.  This scans the entire computer and produces a database /var/lib/aide/aide.db.new.gz.  A copy of this database should be retained as a baseline, in case a forensic investigation occurs.  If possible it should be stored on read-only media, off-line and off-site.  To use this database as your baseline copy it to /var/lib/aide/aide.db.gz, the name of the working database.

To check against the working database, aide -C.  The output is stored in /var/log/aide/aide.log.  Examine the output for unexpected changes, any unexpected changes should be investigated. 

Checking integrity does not update the database, this must be done manually.  Update and archive the database after documented changes (software installation or patches) using aide -u.  

Best practice says that aide should be run daily and the results archived.  This can be accomplished with cron or anacron. A wrapper script that copies the results to a centralized server would be appropriate. 

When setting up checks for multiple machines, it is advisable to offset the start times.  This is particularly important in a virtualized environment, as aide does a full scan of the system each time it is run, and can place a very large load on shared storage. 

Prelinking is a deprecated feature designed to speed performance by altering the linkage sets within executable binaries.  It was found to yield minimal benefit, and under certain circumstances causes system corruption, including full bricking.  Beginning with EL7 prelink is no longer a supported package, and is not installed by default.  But it may be installed on EL6, or if a system administrator followed an out-of-date performance tuning document. 

Because prelinking changes files it will cause false positives when using aide and rpm -V.  This effectively renders any system integrity checks useless.

If prelink has been installed, disable it by creating a file /etc/sysconfig/prelink, with the line PRELINKING=no.  You can then undo the changes it made to binaries by running /usr/sbin/prelink -ua.  When this has completed, yum remove prelink.

FIPS

The FIPS (the Federal Information Processing Standard) is a series of standards to which all government, and other regulated secure systems must conform.  To enable strict compliance with FIPS 140-2 (cryptographic standards), add fips=1 to the kernel command line at installation.  This ensures that all keys are generated with FIPS algorithms and that fips will be enabled on boot.  To verify fips compliance run sysctl crypto.fips_enabled; it should return 1.

There is a published procedure to implement FIPS on an existing system, but it should not be used as it is more likely to break the system than it is to actually secure it.  Also, if you implement FIPS after installation, there is no guarantee that keys generated for the system are made with the proper algorithms and with appropriate entropy sources. 

For best results you should add entropy to the system by inputting some random keystrokes (at least 256) during the installation procedure.

Reference – http://csrc.nist.gov/publications/PubsFIPS.html

oscap, scap-workbench

OpenSCAP (oscap) is an open source security content automation protocol toolkit approved by DISA and NIST as an 'Authenticated Configuration and Vulnerability Scanner'.  It also can perform remediation based on its findings.  This works quite well:  on a default installation of EL7 with "STIG compliant server with GUI" selected as the installed security profile, the number of findings went from 106 down to 19 in minutes.  Installing scap-workbench will install all required packages.  Alternatively you can group install "Security Tools" if optional packages are enabled, or select them during initial server build.

Ideally oscap should be run from a GUI as the command line is complex and poorly documented.  A "simple" command line to scan and remediate EL7 as run from /usr/share/xml/scap/ssg/content looks like this:

oscap xccdf eval --remediate --profile /stig-rhel7-server-upstream 
--cpe /ssg-rhel7-cpe-dictionary.xml /ssg-centos7-xccdf.xml

The command line can get as interesting as:
oscap xccdf eval --datastream-id
      scap_org.open-scap_datastream_from_xccdf_ssg-rhel7-xccdf-1.2.xml
--xccdf-id scap_org.open-scap_cref_ssg-rhel7-xccdf-1.2.xml
--profile xccdf_org.ssgproject.content_profile_C2S
--oval-results --results /tmp/tmp.74oUO0gtVd/results-xccdf.xml
--results-arf /tmp/tmp.74oUO0gtVd/results-arf.xml
--report /tmp/tmp.74oUO0gtVd/report.html
--progress /usr/share/xml/scap/ssg/content/ssg-centos7-ds.xml

That block of text was generated by scap-workbench, the graphical tool.  It can be invoked off the action menu or by running it from a graphical terminal (as root).  While not as powerful and versatile as running oscap directly from the command line, scap-workbench is very straightforward.  Some features of scap-workbench:

*   Local or remote scanning and remediation (via ssh)
*   Multiple profiles to meet industry and government standards including:

    *   United States Government Configuration Baseline (NIAP OSPP v4.0, USGCB, STIG)
    *   U.S. Government Commercial Cloud Services (C2S)
    *   CNSSI 1253 Low/Low/Low Control Baseline for Red Hat Enterprise Linux 6
    *   Criminal Justice Information Services (CJIS) Security Policy
    *   Payment Card Industry – Data Security Standard (PCI-DSS) v3
    *   Upstream STIG for Red Hat Enterprise Linux 6 Server
*   Ability to customize profiles
*   Export of custom profiles to rpm format, allowing remediation of isolated systems

The OpenSCAP team is actually upstream to NIST in the production of content, while being downstream in the policy realm.  That is to say NIST produces a policy, OpenSCAP produces the files that implement the policy (the content), then NIST approves that content.  Content for RHEL6 is available at https://nvd.nist.gov/ncp/checklist/438/download/2556.

There is not a no published content for CentOS6 or other derivative EL6 versions.  For CentOS and Scientific Linux, you can use a conversion script:

*   wget https://raw.githubusercontent.com/OpenSCAP/scap-security-guide/master/shared/utils/enable-derivatives.py
*   chmod 700 enable-derivatives.py
*   ./enable-derivatives.py --enable-centos -i /ssg-rhel6-xccdf.xml -o /ssg-centos6-xccdf.xml

Then run scap-workbench and load the newly created xccdf.  For other flavors of EL you can either modify the script, or simply hand edit the base rhel6-xccdf file as needed.

The SCAP content for EL7 has recently been approved by NIST.  It will be available at https://nvd.nist.gov/ncp/repository.  Pre-release content is available at
https://github.com/OpenSCAP/scap-security-guide/releases/.  Locally stored content will also be updated with the scap-security-guide package. 

This content should be treated as 'trust, but verify' as simply using it does not constitute a full validation.  Much more information is available at https://www.open-scap.org, which also has one of the most readable versions of the STIG (https://static.open-scap.org/ssg-guides/ssg-rhel6-guide-stig-rhel6-server-upstream.html).

Ansible

Ansible is a centralized configuration and automation platform capable of controlling not just EL family Linux hosts, but everything from routers and switches, to Azure and AWS cloud services.  Full documentation is at http://docs.ansible.com, the source for ansible is available at https://github.com/ansible.  Ansible is now a subsidiary of Red Hat.

The Ansible-Lockdown group has produced a STIG compliance playbook, which will perform much of the STIG-requisite configuration for you.  It is primarily this task that we will focus on.

To install and configure on RHEL6:

*   yum-config-manager  --enable rhel-7-server-extras-beta-rpms ; yum makecache   
*   yum install  rhel-system-roles  ansible git

On other EL6 distros:

*   yum install epel-release.noarch; yum makecache
*   yum install ansible git

A simple ansible command looks like this: ansible -m shell -a 'free' all.

Where -m loads the module shell, -a passes the argument 'free' to shell, and all is the target host list.  This will run the command free, via the shell on all listed target hosts.  This command could also have been run as ansible all -a 'free'.

The target host list is in /etc/ansible/hosts, they can be grouped with [brackets]. You will need key-based ssh to each host listed.

The modules control a certain action or type of command.  A full list of modules can be obtained with ansible-doc -l.  For documentation on the shell module: ansible-doc shell.    Use -u to run as an alternate user.  Another useful module is service, the following line restarts httpd on all:
ansible all -m service -a "name=httpd  state=restarted".

While you can call commands directly, the strength of ansible comes from its ability to run playbooks, which call tasks and can produce fully automated workflows.  To obtain the STIG playbook, In an empty directory (such as /gitpath/): 
# git clone --recursive https://github.com/ansible/ansible-lockdown.git

To call the STIG playbook: ansible-playbook -l hosts /gitpath/ansible-lockdown/stig.yml. 

Ansible also has a GUI-based control station called Ansible Tower.  A free limited-feature version can be run for up to 10 hosts.  Red Hat has recently open sourced a version of Tower, called awx, which does not have these limitations. Releases of awx will be developmental, much as Fedora is related to RHEL.  It is anticipated that there will eventually be a stable release version, following the CentOS model.  awx runs only on EL7, and won't install on EL6 as it depends on systemd.  Installation is lengthy and involved; briefly, here are the steps:

*   Verify umask = 0022
*   Install the first set of requisite packages:

    *   yum install

        *   git
        *   epel-release
*   Copy the software to /awx:

    *   cd /
    *   git clone https://github.com/ansible/awx &.
*   Install the rest of the requisite packages:

    *   yum install

        *   python-pip (may not be required)
        *   docker ansible
        *   python-docker-py
        *   make   
*   Clean up a bit before continuing:

    *   yum update; yum clean all; rm -rf /var/cache/yum/; yum makecache
*   Enable docker.service and reboot just for good measure:

    *   systemctl enable docker
    *   reboot
*   Open a hole in the firewall

    *   firewall-cmd --add-service=http
*   Install awx:

    *   cd /awx/installer
    *   ansible-playbook -i inventory install.yml This will take a while.

*   There are several ways you can track the install:

    *   top
    *   watch docker ps
    *   docker logs -f …

        *   awx_sdist_builder
        *   loving_pare
        *   postgres
        *   awx_web
        *   awx_task
    *   open http://localhost in Firefox or Chrome.  Wait for the login screen

        *   default login is admin/password

To use awx to apply the STIG

*   Create a Project

    *   Type: git
    *   Url https://github.com/ansible/ansible-lockdown.git
    *   Update on Launch.
*   Add a Credential

    *   Type: Machine
*   Create a new Inventory

    *   Within that inventory create a Group
    *   Add your Hosts to that group
*   Create a Template

    *   Job type is Run
    *   Select your Inventory
    *   Select the Project you just created
    *   Select stig.yml as your Playbook
*   Launch the Template by pressing the 'rocket' button

clam

Linux systems do not need an anti-virus/anti-malware solution – at least that's what many people will tell you.  With the ever increasing pace of malware development, this is becoming less true by the day.  It is also required by STIG.  There are two acceptable alternatives for provision of virus scan capability:  McAfee VirusScan (the nails service) and clamav.  We will be only dealing with clamav as it is FOSS and included in the epel-repo.  It is not included in the Red Hat distribution or any RHEL maintained repos.  To install it on RHEL, you will need to enable the epel-repo manually.

*   Install the following from the epel repo: 

    *   clamav, clamav-data, clamav-devel, clamav-file system,
        clamav-lib, clamav-scanner, clamav-server, clamav-update. 

*   If not already done, in /etc/clamd.conf

    *   Comment out Example
    *   Uncomment LocalSocket
    *   Uncomment or add

        *   ExcludePath ^/proc/
        *   ExcludePath ^/sys/
        *   ExcludePath ^/sys/
    *   CrossFilesystems no

*   If not already done, in /etc/freshclam.conf 

    *   Comment out Example

*   Run freshclam to update the AV database. 

*   Start and enable the clamd service
    You will receive a warning that Bytecode was disabled, this is ok

*   Run the following with cron at appropriate intervals:

    *   /bin/freshclam

    *   /usr/bin/nice -n 15 /bin/clamscan
        --quiet  / -rol /var/log/clamscan.log

Labs

Lab resources are available at:

https://github.com/janustechacademy/EL6

Lab 1: Initial Configuration

1.  Log into your lab machine.

2.  Install bash-completion.
3.  Logout and log back in to activate bash-completion.
4.  Using redirection ( >, >>, | ) create a file named IP-info which contains the output of the following commands:  ip a, ip route, ip neigh.
5.  From the contents of IP-info create a new file named 192-info.  It should only have lines containing the string 192.
6.  Examine the man pages for: cp, mv, ln, and history.
7.  Create a file called TZ-man which contains a list of all the man pages relating to timezone.
8.  Clear your history list by deleting all entries.
9.  Copy IP-info to IP-old; rename 192-info to 192-old.  Do this on one line.
10.  Insert your history at the bottom of 192-old.
11.  Make a directory (mkdir) called 192-zzz

    1.  cat 192-* – this will return the contents of 192-old, and an error message because cat can't read a directory.

        1.  Create a file err-192 that contains only the error from this command.
        2.  Run the command again, displaying only the error.
12.  Update all software in the background, hiding the output.

Lab 2:  Files and Directories

Finding Things

For the following exercises, unless otherwise specified, you may use any commands you choose to determine the answers.  These might be helpful: locate, whereis, which, and find. 

Record answers in a file /lab/02-Files/results.

1.  Find and record the location of the cp command.

2.  Find and record the location of the man pages for the mv command.
3.  Find all instances of a file called findme.script. 

    1.  How many did you find?
4.  How many instances of this script are in root’s $PATH?
5.  Which version runs when root calls findme.script without a path?  Record the location.
6.  Create a file in /lab/02-Files/ called mxyzptlk.  Use locate to locate it.  Did it work?  If not, fix it.

Finding Things with find

In this section, use the find command to answer the questions.  Put all output in results.

Tip: putting 2>/dev/null after a query will suppress errors from the /proc file system.

7.  The /etc directory contains directories and files that begin with rc and end with .d.  Find only the directories.
8.  Find any unowned files on your system.
9.  Find any files with the SUID bit set which ARE ALSO writable by others.
10.  Find any files which haven’t been accessed in more than 25 years (they do exist!).
11.  Use a single line command to locate and optionally remove the
    /lab/02-Files/killme directory and all its contents.  Do be careful.
12.  Find any file in /boot greater than 20 megabytes in size.

Manipulating Files and Directories

In this section, we will create, manipulate, and destroy files and directories.  You may use any commands you like to achieve these goals.

13.  Create a directory in /lab/02-Files/ called new.
14.  Change directories to new.
15.  Create a file named file1.  Put the phrase “this is file 1” inside of it.
16.  Copy file1 and call the copy file3.
17.  Rename file3 to file2.
18.  Create an empty file called file3
19.  Create a directory in /lab/02-Files/new called subfiles
20.  Use a single command to copy all files in the /lab/02-Files/new directory into subfiles.
21.  Move file1 up one level using dot notation.
22.  Without using vi, read file1 and append its contents to file3. 

Lab 3: vi

1.  vi /lab/03-vi/edit-me, follow the directions in the file.

2.  When complete check your work:
    # diff edit-me edit-me.finished | grep "<" .
    The result should be just the date and your name

3.  Set the hostname on both your computers in /etc/sysconfig/network.  Reference the student handout for naming information.  Reboot to make the change effective across all sessions.
4.  Set a static IP address for both computers:

    1.  Find your active network card using ip a | grep 192 .
    2.  Make a backup of the appropriate file
        cp /etc/sysconfig/network-scripts/ifcfg-ethX /etc/ifcfg-ethX.bak (where ethX is your active network card)
    3.  vi /etc/sysconfig/network-scripts/ifcfg-ethX
        Use the static addressing information provided on your student sheet. It should look something like this:

DEVICE=eth2

TYPE=Ethernet

ONBOOT=yes

NM_CONTROLLED=no

BOOTPROTO=static

IPADDR=192.168.1.160

NETMASK=255.255.255.0

GATEWAY=192.168.1.1

DNS1=192.168.1.251

DNS2=192.168.1.252

4.  Restart the network service: service network restart
5.  Start a session to the new IP address.  Be patient, initial ssh setup may take a few seconds longer than expected.
6.  Remove your backup files from /etc/ .

Lab 4: Users and Groups

1.  Configure your computer such that users are created with:

    1.  default password expiration of one month from now
    2.  immediate inactivation on password expiration
    3.  password aging fields and logon failure delay meets standards
    4.  Do not set minimum password length or quality requirements at this point.
2.  Enable wheel in sudoers.
3.  Configure /etc/pam.d/su to restrict use of su - to members of wheel.
4.  Edit /etc/skel/.bash_profile to contain this line
    script -c "/usr/bin/screen -RL" /dev/null
5.  Create the following users as specified.
    Unless otherwise stated, all should have a primary group of their own.
    All users should have a password set.
    Usernames should be all lower case.

    1.  Adam and Brenda – regular users
    2.  Don and Emma – can use sudo,  members of group dev.
    3.  Frank – cannot login interactively, with a comment noting that fact.
    4.  Grace – UID = 3001, member of dev, helpdesk, and recruiting
    5.  Harry – UID = 3002, member of recruiting, lock his account.
    6.  Jane and Mary – members of recruiting and restricted-users
    7.  Nick – member of helpdesk.
6.  Try to log in as Frank.
7.  Set Harry's home directory to /lab/05-Permissions/recruiting.
8.  Add Grace to group wheel.
9.  Change Brenda's shell to vi.  Change to her environment.

    1.  Attempt to read the date into a file – what caused the failure?
10.  Check your work by viewing the relevant files in /etc/.

Lab 5:  Ownership, Permissions, and Access

1.  Preparation:

    1.  Ensure that grace is a member of helpdesk, but NOT recruiting. 
    2.  Ensure that harry is a member of recruiting, but NOT helpdesk. 
2.  Setting Ownership and Basic Permissions

    1.  As root, create the following directories:  /lab/05-Permissions/recruiting, /lab/05-Permissions/helpdesk
    2.  Assign ownership of recruiting to user harry and group recruiting.
    3.  Assign ownership of /lab/05-Permissions/helpdesk to user grace and group helpdesk.
    4.  As harry, set the permissions of recruiting to 770.
    5.  As harry, set the access mode of recruiting so that new files in that directory will automatically be owned by the recruiting group.
    6.  As grace, set the permissions of helpdesk to 770.
    7.  As grace, set the access mode of helpdesk so that new files in that directory will automatically be owned to the helpdesk group.
    8.  As grace, attempt to access the recruiting directory.  This should fail.
    9.  As harry, attempt to access the helpdesk directory.  This should fail.

3.  Extended ACLs – The order in which you do these tasks matters, as some ACL commands may overwrite previous entries.  Review the exercise first, and plan your ACLs before applying them. 

    1.  Create a file in recruiting called rfile.  It should contain the line, “this is rfile.”
    2.  Create a file in helpdesk called hfile.  It should contain the line, “this is hfile.”
    3.  Set an extended ACL on recruiting that will allow members of the helpdesk group to list the contents of the directory and read the files inside of it. 

        1.  Grant full control of any files created in this directory to grace. 
        2.  Others should have no access.
    4.  Set an extended ACL on helpdesk that will allow members of the recruiting group to list the contents of the directory and read the files inside of it. 

        1.  Grant full control of any files created in this directory to harry. 
        2.  Others should have no access.
    5.  Mask away execute permissions for any files created in these directories.
    6.  Ensure that these ACLs are applied recursively to the existing files in the directories.
4.  Testing SUID

    1.  Verify that all executables in /lab/05-Permissions are SUID/SGID root:root
    2.  su - adam.
    3.  Run who, id, and whoami.  Note the results.
    4.  cd /lab/05-Permissions.
    5.  Run who, id, and whoami again.  Note the results.
    6.  Run those three commands once again, this time with a ./ preceding each.
    7.  Add . to the beginning of Adam's path.  Run the commands one last time, this time without the leading ./

Lab 6:  Regular Expressions

You will find the files for this exercise in /lab/06-regex.

1.  Copy something.com.zone to else.com.zone.

2.  Copy something.named.conf to else.named.conf.
3.  Take a moment to read over these two files and familiarize yourself with their contents.
4.  Display any lines in else.com.zone which contain IP addresses. 

    1.  Place the result in else.ip.
5.  Display any lines in else.com.zone which contain hostnames.

    1.  Place the result in else.host.
6.  Repeat these tasks for the else.named.conf file.

    1.  Append the results to else.ip and else.host.
7.  Your network has been renumbered from 192.168.10 to 10.10.10.  Use sed to make the appropriate changes IP addresses in the else.com.zone and else.named.conf file.
8.  You have a new domain.  Your old domain something.com is being replaced with else.com  Use awk to make the appropriate changes in both files. 

    1.  This includes both hostnames and filename references. 
    2.  DO NOT change any references to domains other than something.com.
    3.  Do not alter any portion of a hostname OTHER THAN the something.com domain.
9.  Take a moment to review your work.  Compare the new files to the originals.  Did you miss anything?  Did you accidentally change anything you shouldn’t have?  If you did, resist the urge to hand correct this with vi.  Try to use sed or awk to fix mistakes.

Pointless Fun

If you finished early, and you need something to do, try this:

11.  Copy /etc/passwd to /lab/06-regex/passfile
12.  Use sed to remove all lines in passfile that start with a and save the file in place.
13.  Use diff to compare passfile and /etc/password. 
14.  Display passfile, sorted alphabetically, saving a copy to alphapass in one line. 
15.  Display alphapass to your screen, but replace all the colons with linebreaks. 
16.  Repeat the last step, but eliminate duplicate lines. 
17.  Repeat the last step, but only show lines that start with a slash. 

Lab 7:  File Systems

Throughout this lab, you will be making extensive changes to disk structures.  Please remember to check your work and ensure that the kernel is aware of your changes.  If it is not, provoke rescans of your SCSI bus using the methods supplied in the course manual.

1.  Partitioning with fdisk

    1.  You should have an empty hard drive attached to your system.  Identify it.
    2.  On your free disk, create 3 partitions of 1 GB each.
    3.  Ensure that the partition table is updated to reflect your work.

2.  File System creation and mounting

    1.  Put an ext4 filesystem on your first empty partition.
    2.  Add ACL support to this filesystem.
    3.  Create a mountpoint called /mount1.
    4.  Mount the filesystem to /mount1.
    5.  Check it.
    6.  Unmount the filesystem
    7.  Configure /etc/fstab to automatically mount your new filesystem at boot or by mountpoint.  Use default options.
    8.  Mount your new filesystem with: mount /mount1 .
    9.  Check your work.
3.  LVM

    1.  Create a physical volume from your second partition.
    2.  Create a volume group containing only that physical volume.
    3.  Create a logical volume that uses 100 percent of the free space in that volume group.
    4.  Create an ext4 filesystem on that logical volume.
    5.  Add ACL support to the new filesystem.
    6.  Create a mount point /mount2 and mount the filesystem to it.
    7.  Unmount it.
    8.  Put it in /etc/fstab.
    9.  Mount it.
    10.  Pretend the filesystem is full.  Use the 3rd free partition to extend the volume group, logical volume, and filesystem.

4.  Hard Links

    1.  Create a file in /lab/07-Filesystems/ named original, with content:  “This is the original file.”
    2.  Create a hard link to the file in the same directory.  Call the link copy. 
    3.  Get a list of inodes for all files in /lab/07-Filesystems.  What are the inode numbers for original and copy?  Record the inode of original.
    4.  Read the contents of copy.  What does it say?
    5.  Add a line to copy that says, “edited from copy.”
    6.  Read the contents of original to the screen.  What does it say?
    7.  What is the link count for original?  What is it for copy?
    8.  Delete original.
    9.  What is the link count for copy?
5.  Symbolic Links

    1.  Create a symbolic link to copy in the same directory.  Call the link original.
    2.  What are the inodes of the files?  What does a long listing tell you about original?
    3.  Move original to /mount1/original. 
    4.  Add a line to original that reads, “edited from symbolic original”. 
    5.  Read copy.  What does it say?
    6.  What is the link count for copy?
    7.  Delete copy.  Attempt to read /mount1/original.  What happened?
    8.  Create a file in 07-Filesystems called copy. 
    9.  Add a line to it that reads, “this is not the same file.” 
    10.  Attempt to read /mount1/original.  What happened?
    11.  Delete /mount1/original.  
    12.  Read copy.  Did deleting /mount1/original have an effect on /lab/copy?
    13.  Make a hard link from /lab/07-Filesystems/copy to /lab/07-Filesystems/original.
    14.  Delete /lab/07-Filesystems/copy.  What are the contents of original?  What is the inode and link count?  Does the inode for original match the one recorded earlier in this lab?

Lab 8: Processes and Services

1.  Preparation

    1.  Open at least three connections to your server.  You may even want more.
    2.  Run top in one session…you will want to keep top open throughout this lab.
    3.  All scripts are in /lab/08-Process and are described in; alter permissions as needed.
    4.  Read through the instructions before executing any given step.
    5.  Verify who you are before running memmy.  If run as root, it will break your box.

2.  Pause top; open vi, and man top – in the same window. 

    1.  Toggle between them using jobs and fg.

3.  Run chew, this will execute bc (a calculator) – using quite a bit of cpu.  Note its PID.

    1.  Using the signal passing function of top, pause and resume the bc process.
    2.  Background the bc process from the command line that originated it.
    3.  disown it and log out.  Did it continue running?

4.  Start spread, this will run the command bc backgrounded at varying nicenesses.

    1.  Create a file with the PIDs of the bc process in it
    2.  Pause all of them except the nicest.

        If you get really stuck on this there are hints in /lab/08-Process/killer.

    3.  Resume the 5 least nice.
    4.  Clean up all the bc processes before proceeding.

5.  Start a watch for processes named sleep.  In a separate window watch for processes belonging to jane.

    1.  Run nappy as root, Jane, and Mary.  This starts multiple sleeps.
    2.  Run spread as Jane.

        1.  What is different when Jane runs spread?
    3.  Kill all of Jane's sleep processes, without affecting any others.
    4.  Kill all of Mary's processes.
    5.  Clean up the bc and sleep processes before proceeding.

6.  Give Mary a hard limit of 1 minute cpu.  Set hard limits on Nick for nproc = 5000, nice and priority =15.

    1.  As Mary, run chew.  Observe what occurs when processor time hits 60 seconds.
    2.  As Nick, run spread.  Notice the priorities.
    3.  As Nick run forkbomb.
    4.  Clean up all of Nick and Mary's processes.

7.  Start a vmstat -a -S M 5. This will display memory information in MiB.

    1.  Run swapoff -a, watch the swap file drain.  Confirm that swap was disabled using swapon --summary.
    2.  In a new window prepare to issue pkill grep, do not pressenter yet.
    3.  As Mary, run memmy. 

        1.  Observe the change in memory usage.
        2.  As soon as Out of memory errors begin, pkill grep .
        3.  Near the end of /var/log/messages, search for oom-killer. Then read down from there.
    4.  Re-enable swap.
    5.  Run memmy again as Mary.  Observe the differences.
    6.  To ensure that no rogue processes are left over, reboot.

Lab 9 : Scheduling Events

1.  All tasks for this lab are in /lab/09-Events

    1.  Set ownership and permissions such that Nick and Mary can run these tasks.
2.  Allow Mary and Nick the ability to create at and cron jobs.
3.  Using at have Mary schedule

    1.  at.task1 five minutes from now
    2.  at.task2 a few minutes after midnight tonight
    3.  at.task3 an hour from now and Friday afternoon
    4.  at.task4 next Tuesday at 11 am
    5.  View the jobs.
    6.  Remove the job which would run at.task3 Friday afternoon.
4.  Using cron have Nick schedule

    1.  cron.job1 weekly beginning ten minutes from now
    2.  cron.job2 at 2130 on odd numbered dates during the week
    3.  cron.job3 at the most infrequent interval possible
    4.  cron.job4 at 1130 on weekdays
5.  As root, use anacron and a symbolic link to run cron.job5 weekly
6.  Lower the batch threshold to 0.01

    1.  Run chewy from the previous lab
    2.  Create a batch job that will wall "Done with this lab!"
    3.  End the bc processes started by chewy

Lab 10: Booting

1.  Make a copy of grub.conf
2.  Alter the copy to:

    1.  Have a timeout of 15
    2.  Not hide the menu
    3.  Have a new boot entry called Other which

        1.  Displays all boot messages
        2.  Has SELinux disabled
3.  When done have an instructor verify your changes.

Note: there is no Lab 11.

Lab 12:  SELinux

We’ll be working with Apache and SELinux in this lab.  The httpd daemon should already be installed, and the configuration files on your machines should already be altered to allow the labs to function as written.  You should only need to make changes of an SELinux nature to accomplish the stated goals. 

1.  Using Booleans

    1.  Become user grace.
    2.  In grace’s home directory, create a new directory called public_html.
    3.  Set the permissions on this directory to 755.
    4.  Create a new file in ~/public_html called index.html.  The contents of index.html should be a single sentence, reading, “Successfully viewed the file via home dirs.”
    5.  Set the permissions of index.html to 744.
    6.  Become root.
    7.  Temporarily disable the firewall: service iptables stop.  In later modules, we will learn how to properly configure firewall rules.  For now, this is sufficient.
    8.  Attempt to access this address: http://hostname/~grace/
    9.  This should fail.  Take any steps necessary to resolve the issue.

2.  Setting a Security Context on Files and Directories

    1.  Create a directory, /web with permissions of 755
    2.  In /web create index.html, with permissions of 744 and content  “Successfully viewed the file in /web.”
    3.  Edit /etc/httpd/conf/httpd.conf. Change the following lines to reflect the new Document Root of /web:

DocumentRoot "/var/www/html"

<Directory "/var/www/html">

4.  Restart the httpd service.
5.  Attempt to access this address: http://server-name/
6.  What happened?  Did you get the results you were expecting?
7.  Take any steps necessary to resolve this issue.

3.  Altering Security Contexts for Ports

    1.  Edit /etc/httpd/conf/httpd.conf. Change the line Listen 80 to Listen 8000.
    2.  Restart the httpd service.
    3.  Attempt to access http://server-name:8000
    4.  What happened?  Were these the results you were expecting?
    5.  Take any steps necessary to resolve the issue.
4.  Turn your firewall back on, shut down httpd, and check that SELinux is enforcing.

Lab 13: Networking

1.  Confirm that the NetworkManager service is uninstalled.

2.  Configure your networking control files:

    1.  Configure /etc/resolv.conf to search the namespace VM.NOT.
    2.  Ping the other student's machines by FQDN and by single name.
    3.  Create a file called /lab/13-Network/netinfo with your neighbors hostnames, ip addresses, and MAC addresses thus:
        duh.vm.not – 192.168.1.48 – 00:50:56:87:49:49 .
3.  Find the name server (NS) and mail exchanger (MX) names and addresses for redhat.com, and doe.gov.  Append this to netinfo.
4.  Using ss, start a watch on all tcp ports.

    1.  ssh to yourself, then ping yourself.  Why is there a difference in the ss output?
    2.  Run ss by itself (without watch), modifying the results to exclude listening ports and connection from ::1, and include process information. 
        Append this to netinfo.

5.  Getting to STIG – Pay special attention to the order of the rules in your chains.

    1.  Create an at job to disable the firewall 20 minutes from now.  If you haven't locked yourself out, remove and renew the job every now and then.  If you do lock yourself out, it will let you back in when it runs.

        Note: the most common method of locking yourself out is by creating a default DROP with no other rules configured.

    2.  Configure your INPUT chain to have a default policy of DROP.  Remove or replace any rules in the INPUT chain which would interfere with the default DROP action.
    3.  Configure your FORWARD chain to have a default policy of DROP.  Remove or replace any rules in the FORWARD chain which would interfere with the default DROP action.
    4.  Ensure that the iptables service is running.
    5.  Set iptables to start on boot at run levels 2,3,4, and 5.

6.  Opening and Closing Ports for httpd

    1.  Allow https on TCP port 443 inbound from anywhere, for NEW, ESTABLISHED, and RELATED connections.
    2.  Block http on TCP port 80 inbound from anywhere.
    3.  Test these rules from your windows box.
7.  Allowing NFS

    1.  NFS v4 requires TCP port 2049.  Allow new incoming connections to TCP 2049 ONLY from the IP of your windows box (windows IP can be determined by running ipconfig from command line).
8.  Allowing VNC Server

    1.  VNC server requires base TCP ports of 5800, 5900, and 6000 to be open.  Configure rules to support this.
    2.  VNC also requires sequential ports to be opened per user session.  To support two user sessions, we will need the following tcp ports opened: 5801, 5802, 5901, 5902, 6001, and 6002.  Configure rules to accept this traffic.
9.  Finishing Up

    1.  Issue any commands required to save your iptables configuration.  Restart the iptables service.

Note: There is no Lab 14.

Lab 15:  Remote File Systems

1.  Initial Configuration of NFS Server and Client

    1.  In /etc/sysconfig/nfs set
        RPCMOUNTDOPTS="-N 2 -N 3"
    2.  In /etc/nfsmount.conf uncomment the following:
        # Defaultvers=4
        # Nfsvers=4
        # Defaultproto=tcp
        # Proto=tcp

2.  Making the Shares

    1.  Create a directory: /hdshare
    2.  Set ownership to grace:helpdesk and permissions to 2775.
    3.  Create a single file in this directory.  Name it heybuddy.  Include a message for your partner.
    4.  Share /hdshare to your partner with read/write access, and default options.
3.  Mounting and Using NFS

    1.  Create a local directory: /netshare
    2.  Mount your partner’s shared directory to /netshare.
    3.  As root, attempt to access the share.  Attempt to read and edit heybuddy. 
    4.  As grace, attempt to access the share.  Attempt to read and edit heybuddy.
    5.  Unmount the share.
    6.  Add the share to /etc/fstab.
    7.  Mount it using the local mount point name only.

Lab 16: Remote Access

1.  Provide vnc service for Adam and Grace.

    1.  Log into your machine using tigervnc supplied in the /labs/16-Remote directory as both Adam and Grace.
    2.  Verify that access persists over a reboot, without needing to log in via ssh first.

2.  Secure sshd, provide a login banner.

    1.  Work with one of your neighbors to ssh without password as Grace and root from one machine to the other.
    2.  Use scp to copy the netinfo file you generated earlier to /labs/16-Remote on your neighbors machine.
3.  Restrict Adam to sftp only. 

    1.  Create a chrooted sftp home directory for him. 
    2.  Move a copy of your local /etc/hosts to Adam's home directory on your neighbor's machine.
4.  Create a file showing all nonroot logins which have occurred on your computer.  Make it available via http.

    1.  Get a copy of a classmates file, without using a graphical browser.

Lab 17:  Kernel Modules and Parameters

1.  Listing Kernel Modules and Tracing Dependencies

    1.  In your terminal, display a list of currently loaded kernel modules.
    2.  Locate bnx2fc.
    3.  Display more detailed information about bnx2fc.  What does the description tell you about it?  Does it have any associated parameters?
    4.  What is the default value of bnx2fc’s debug_logging parameter?  Is that the currently loaded value?  Verify this.
    5.  Attempt to alter the debug_logging parameter of bnx2fc to reflect a value of 0x01 without unloading the module first.  Did this succeed?  Why or why not?
    6.  Are there any other modules that depend on bnx2fc? 

2.  Loading and Unloading Kernel Modules

    1.  Unload bnx2fc.  Did any other modules unload with it?  Why or why not?
    2.  Attempt to load bnx2fc with the debug_logging parameter set to 0x01.  Did this succeed?  Verify it.
    3.  Unload the module again.
    4.  Make any changes necessary to cause bnx2fc to load with a debug_logging parameter value of 0x02 when next loaded.
    5.  Load it.  Did the changes take?  Why or why not?
3.  Blacklisting Modules

    1.  Unload bnx2fc.
    2.  Blacklist the module.  Ensure that this module will not be loaded either manually or automatically.
    3.  Test it.

Lab 18: Disaster Recovery

1.  Create compressed archives of /lab called lab.tar and /etc called etc.tar, preserving all attributes

    1.  Restore the lab.tar to a new directory /new-labs/
    2.  Create an archive of all files changed in /etc and /lab in the last two days.  Place it in /lab/18-disaster/.
    3.  Delete /lab/03-vi/editme.finished
    4.  Add a file /lab/03-vi/editme.added
    5.  Compare the lab.tar with the current filesystem using tar.
2.  rsync all .conf files from /etc/ to /new-labs/saved-confs on your neighbor's machine.

    1.  Delete /etc/sane.d/ on your machine.
    2.  Add a comment to /etc/asound.conf
    3.  Restore sane.d without overwriting your changes to asound.conf

Lab 19: Security

1.  Install and configure aide.

    1.  Write a script to be run daily which archives your results on a neighbor's machine.

2.  Configure clam anti-virus to run on a regular basis.
3.  Audit your installed software and services. Write a series of removal recommendations in /lab/19-Security/software-clean.

    1.  Don't forget to check dependencies, don't remove things that would break functionality.
    2.  Outline further steps you would take to secure this machine.
    3.  Be prepared to justify your results

Lab 20 – Final

You have just inherited a new computer.  It has been severely misconfigured, and may have been compromised.

Your new box is currently only reachable by telnet, and is drawing a DHCP address.  Your instructor will provide you its current address, as well as the static addresses and hostname that it should be given. 

Current logins are student and root, both with password ujm<KI*(98.

You will have the use of one of the computers you used during the class, access to the Internet, the course materials, and any notes you have made during the course. 

You must secure the computer.  You will be given a subset of the STIG as the standard for security.  Your machine must be as compliant as possible to the attached Security Standards. 

Some features and functionalities must also be added. 

All security and functionality should work without intervention after a reboot.

Create brief documentation of your success or failure for each step in /lab/20-Final/notes.txt.  If there are multiple possible ways of accomplishing a task, note the method used.

It is recommended that you review all tasks and the Security Standards before beginning.

1.  Configure your IP addresses and hostname.

2.  Establish secure communication with your box. 

    1.  Restrict ssh to your local network.
3.  The firewall and SELinux must be properly configured.
4.  The boot sequence should be protected from unauthorized meddling.

    1.  set the password to BootMe
5.  Create two partitions of approximately 400 MB each on the second drive.
6.  One of these partitions should be used as the base directory for web services. 

    1.  This file system should

        1.  be mounted at /new-web
        2.  be labeled web
        3.  be mounted by label rather than device name.
    2.  Create an index.html with the text "This is a test".
    3.  index.html should only be viewable from your subnet.
    4.  Share /lab/20-Final/notes.txt via the web, without moving or copying it.
7.  Dave has been terminated.  His account should be dealt with.
8.  Create these users:

    1.  Kate – member of group staff and developers
    2.  Mike – member of group developers, account expires at the end of the year
    3.  Nick – member of developers and helpdesk, UID = 4001
    4.  Paul – UID = 4002, shell = vim
9.  In the second new partition create a shared directory /home/code for the developers. 

    1.  Allow all members of developers, except Nick, read/write access to code.
    2.  Nick should have read access only.
    3.  Users should not be able to delete files owned by another user.
    4.  Any new files or directories created in code should

        1.  be owned by the creator and by the developer group
        2.  have appropriate permissions
10.  Provide VNC access for Nick.
11.  Allow only Kate and Mike the ability to use sudo.
12.  Restrict direct root login to only tty1.
13.  Configure certificate-based login from class computers to your new box for Kate.
14.  Create a new 200 MB swap file on the second hard drive using a logical volume.  Add it permanently to the current swap space.
15.  Configure aide to run every day at 11 PM. 
16.  Configure yum to remove all metadata and caches, and create a new cache weekly.

    1.  If the computer is powered off, the task must run when it is next powered on.
17.  The system must be fully up to date.

    1.  If a new kernel is available, it should be installed as the default
    2.  The old kernel must remain available and bootable
18.  Restrict the use of cron and batch to root, Kate, and Mike.

    1.  If new users are created, they should not be granted access to cron or batch
19.  Configure ntp to use an NIST server or another server as directed.
20.  Configure your new machine to send log files to your class machine.
21.  Disable ping to your machine.

Security Standards for Final Lab

(A subset of the Centos6 STIG guide at https://static.open-scap.org/ssg-guides.)

22.  Verify that Shared Library Files Have Restrictive Permissions

System-wide shared library files, which are linked to executables during process load time or run time, are stored in the following directories by default:

/lib

/lib64

/usr/lib

/usr/lib64

Kernel modules, which can be added to the kernel during runtime, are stored in /lib/modules. All files in these directories should not be group-writable or world-writable. If any file in these directories is found to be group-writable or world-writable, correct its permission.

23.  Verify that All World-Writable Directories Have Sticky Bits Set   

When the so-called 'sticky bit' is set on a directory, only the owner of a given file may remove that file from the directory. Without the sticky bit, any user with write access to a directory may remove any file in the directory. Setting the sticky bit prevents users from removing each other's files. In cases where there is no reason for a directory to be world-writable, a better solution is to remove that permission rather than to set the sticky bit.

24.  Ensure All Files Are Owned by a Group   

If any files are not owned by a group, then the cause of their lack of group-ownership should be investigated. Following this, the files should be deleted or assigned to an appropriate group.

Unowned files do not directly imply a security problem, but they are generally a sign that something is amiss. They may be caused by an intruder, by incorrect software installation or draft software removal, or by failure to remove all files belonging to a deleted account. The files should be repaired so they will not cause problems when accounts are created in the future, and the cause should be discovered and addressed.

25.  Ensure All World-Writable Directories Are Owned by a System Account

All directories in local partitions which are world-writable should be owned by root or another system account. If any world-writable directories are not owned by a system account, this should be investigated. Following this, the files should be deleted or assigned to an appropriate group.

26.  Ensure SELinux Not Disabled in /etc/grub.conf

Disabling a major host protection feature, such as SELinux, at boot time prevents it from confining system services at boot time. Further, it increases the chances that it will remain off during system operation.

27.  Ensure SELinux State is Enforcing    

The SELinux state should be set to enforcing at system boot time.

Setting the SELinux state to enforcing ensures SELinux is able to confine potentially compromised processes to the security policy, which is designed to prevent them from causing damage to the system or further elevating their privileges.

28.  Configure SELinux Policy    

The SELinux targeted policy is appropriate for general-purpose desktops and servers, as well as systems in many other roles.

Other policies, such as mls, provide additional security labeling and greater confinement but are not compatible with many general-purpose use cases.

29.  Verify Only Root Has UID 0    

If any account other than root has a UID of 0, this misconfiguration should be investigated and the accounts other than root should be removed or have their UID changed.

30.  Set Boot Loader Password    

During the boot process, the boot loader is responsible for starting the execution of the kernel and passing options to it. The boot loader allows for the selection of different kernels - possibly on different partitions or media. The default Red Hat Enterprise Linux boot loader for x86 systems is called GRUB. Options it can pass to the kernel include single-user mode, which provides root access without any authentication, and the ability to disable SELinux. To prevent local users from modifying the boot parameters and endangering security, protect the boot loader configuration with a password and ensure its configuration file's permissions are set properly.

31.  Verify iptables Enabled    

The iptables service shall be enabled.

32.  Rsyslog Logs Sent To Remote Host    

If system logs are to be useful in detecting malicious activities, it is necessary to send logs to a remote server. An intruder who has compromised the root account on a machine may delete the log entries which indicate that the system was attacked before they are seen by an administrator.

However, it is recommended that logs be stored on the local host in addition to being sent to the loghost, especially if rsyslog has been configured to use the UDP protocol to send messages over a network. UDP does not guarantee reliable delivery, and moderately busy sites will lose log messages occasionally, especially in periods of high traffic which may be the result of an attack. In addition, remote rsyslogmessages are not authenticated in any way by default, so it is easy for an attacker to introduce spurious messages to the central log server. Also, some problems cause loss of network connectivity, which will prevent the sending of messages to the central server. For all of these reasons, it is better to store log messages both centrally and on each host, so that they can be correlated if necessary.

Along with these other directives, the system can be configured to forward its logs to a particular log server by adding or correcting one of the following lines, substituting loghost.example.com appropriately. The choice of protocol depends on the environment of the system; although TCP and RELP provide more reliable message delivery, they may not be supported in all environments.

33.  Enable rsyslog Service    

The rsyslog service provides syslog-style logging by default on Red Hat Enterprise Linux 6.

34.  Disable xinetd Service    

The xinetd service can be disabled

35.  Uninstall xinetd Package    

The xinetd package can be uninstalled

36.  Disable telnet Service    

The telnet service can be disabled with the following command:

37.  Uninstall telnet-server Package    

The telnet-server package can be uninstalled

38.  Disable DHCP Client    

For each interface on the system (e.g. eth0), ensure that dhcp is disabled.

DHCP relies on trusting the local network. If the local network is not trusted, then it should not be used. However, the automatic configuration provided by DHCP is commonly used and the alternative, manual configuration, presents an unacceptable burden in many circumstances.

Command Summary

Module 0:  Introduction to Linux

*   ls – list files

    *   -l – long
    *   -a – all
    *   -d – directory
    *   -Z – selinux
    *   -i – inode information
*   cd – change directory

    *   . – this directory
    *   .. – the parent directory
    *   ~ – the home directory
*   pwd – print working directory
*   cat – print a file

    *   -n – number lines
    *   -b – number non-blank lines
*   uname – print system information

    *   -a – all
*   exit, logout, CTL-d – ways to end a shell
*   --help – standard short help option
*   man – manual pages

    *   -k – find man pages about a string
*   makewhatis – update man page database
*   info – documentation

Module 1:  Getting around in EL6

*   yum – software manager

    *   -y – yes
    *   update
    *   install
*   history
*   !! – last command
*   !$ -- last argument
*   $? – last exit code
*   CTL-c – end current command
*   ping – send echo request to a host
*   ssh – connect to a host
*   echo – display something
*   less – view output one page at a time
*   grep – get regular expression
*   ip – view network information

    *   a – address
    *   route – routing table
    *   neigh – neighbors (arp table)

*   a | b  – send output from command a to command b
*   a > x – overwrite file x with output of command a
*   a >> x – append output of a to file x
*   ; – separate commands on a line
*   a && b –run b if a succeeds
*   a || b – run b if a fails
*   & -- run a command in the background
*   0 – STDIN
*   1 – STDOUT
*   2 – STDERR
*   2>&1> /dev/null – suppress all output

*   screen

    *   CTL-a – hot key, repeat to toggle windows
    *   x – lock screen
    *   c – create new
    *   n / p – next / previous
    *   -RL – Reattach if available, and Log

Module 2:  Files and Directories

*   file – determine file type
*   stat – display file status (metadata)
*   which – locate first command in $PATH
*   whereis – search for a command and related files
*   locate – find files based on an index database

    *   updatedb – update the locate database
*   head – display the top of a file
*   tail – display end of a file

    *   -f -- follow
*   wc – word count

    *   -l – count lines
*   find   

    *   -maxdepth / -mindepth
    *   -type
    *   -name
    *   -iname – case insensitive name
    *   -nouser – unowned
    *   -o – OR (default is AND)
    *   -perm – permissions
    *   -atime, -ctime, -mtime – access, change, modify time

        *   -1 = last 24 hours
        *   1 = 24-48 hours
        *   +1 = more than 48 hours
*   dmesg – print kernel ring buffer (boot messages)
*   touch – change file timestamps, create empty file
*   tee – split output to STDOUT and a file
*   column – put lists into columns
*   rm – remove file

    *   -r – recursively
    *   -f – force
*   mkdir – make directory

    *   -m – mode (permissions)
    *   -p – create path if not extant
*   rmdir – remove directory
*   cp – copy

    *   -Z – preserve original selinux context
*   mv – move

    *   -Z – assume destination selinux context
*   sort

    *   -n – numerically
    *   -r – reverse
    *   -u – unique
*   tr – translate characters
*   uniq – find unique lines
*   diff – compare two files

Module 3:  vi

*   Normal – command mode; ESC

    *   u – undo
    *   ctrl-r – redo
    *   yy – yanks (copy)
    *   dd – delete / cut
    *   p – paste
    *   : commands

        *   w – write
        *   q – quit
        *   a – all
        *   ! – force
        *   ! cmd – run command
        *   e – edit from last write
        *   n / N – next / previous file
        *   split / vsplit
        *   r – read
        *   r ! cmd – read command into file
        *   abbr – abbreviate
        *   set number – turn on line numbering, ! turns it off
*   Visual – select mode; v, V, CTL-v

    *   y – copy
    *   d – delete
    *   p – paste
*   Insert – typing mode; i, o, A

*   service – control services

    *   restart
    *   stop
    *   start
    *   status
    *   --status-all

Module 4:  Users and Groups

*   useradd

    *   -G – additional groups
    *   -u / -g – uid / gid
    *   -s – shell
*   passwd

    *   -l / -u – lock / unlock
    *   -S – status
*   chage – change password expiration

    *   -l – list
*   usermod

    *   -aG – add to Groups
*   userdel

    *   -r – remove home directory
*   vipw, vigp, visudo – editors for special files
*   groupadd
*   groupmod
*   groupdel
*   groupmems

    *   -g – groupname, mandatory
    *   -a / -d – add /delete
    *   -l – list
*   whoami – show current user
*   id – show real and effective uid
*   su – change current uid

    *   su - – use destination environment
*   sudo – change effective uid to root
*   who – is currently logged on
*   w – who plus stats and current command
*   uptime
*   lastlog – last logins
*   last – successful logins
*   lastb – bad logins

Module 5:  Ownership, Permissions & Access

*   chmod – change permissions

    *   r = 4
    *   w =2
    *   x = 1
    *   SUID   = 4 (s)
    *   SGID   = 2 (s)
    *   Sticky = 1 (t)
    *   u, g, o, a – user, group, other, all
*   umask – permissions to unset
*   chown / chgrp – change ownership
*   getfacl – get file ACL
*   setfacl – set file ACL

    *   -m – modify an ACL
    *   -x – remove an ACL entry
    *   -b – remove all ACLs for file
    *   -R – apply ACL recursively through subdirectories
    *   [d]:u|g|o|m:UID|GID::perms

        *   d – default
        *   u, g, o – user, group, other
        *   m – mask
        *   UID,GID
        *   perms – rwx permissions

Module 6:  Regular Expressions

*   Common

    *   [a-z] – any single lowercase alpha character
    *   [A-Z] – single uppercase alpha character
    *   [abc] – a, b, or c.
    *   [0-9] – any single digit
    *   [^a2] – any character NOT a or a 2
    *   . – any single character other than line break
    *   [.] – a literal period 
    *   [a|b] – a OR b
    *   ^/$ –  beginning / end of line

    *   Match the preceding…
    *   ? – 0 or 1 times
    *   * – 0 or more times
    *   + – 1 or more times
    *   {N} – exactly N times
    *   {N,} – N or more times
    *   {N,M} – between N and M times

    *   ( )Encloses the pattern to store matches from
    *   \NReturn the match from the Nth (1-9) stored backreference

*   grep

    *   -v – invert the match (return ONLY lines where pattern was NOT matched
    *   -o – match entire line (rather than within the line)
    *   -b – respect word boundaries
    *   -i – case insensitive
    *   -E – extended grep
    *   + ? | {} () – literals in basic grep, metacharacters in extended (-E)

*   sed

    *   -n – prevent normal output printing
    *   -i – perform an in-place edit
    *   -r – extended regular expression mode
    *   -e – multiple expressions in a line
    *   -f – run a sed script.  sed -f script original changed
    *   p – print
    *   s – substitute
    *   d – delete
    *   g – global

        *   sed 's/pattern/replacement/g' filename

*   awk '{ commands }' filename .

    *   Commands

        *   print – print matches
        *   sub()– substitute, once per line
        *   gsub() – global substitute
    *   -F – set delimiter
    *   -f – run a script
    *   /pattern/match a pattern (occurs before commands portion)

    *   Variables

        *   $0 – entire current record
        *   $n – where n is a number; field by sequence e.g. $1,$2
        *   NF – number of fields in current record
        *   NR – number of current record
        *   FNR – if multiple input files, record number of current file
        *   FS/RS – input field separator/record separator
        *   OFS/ORS – output field separator/record separator
        *   FILENAME – the name of the input file; undefined in BEGIN block

    *   Scripting Constructs

        *   BEGIN Run first, used to make header or set variables.
        *   BODY Where the bulk of the script resides.
        *   END Run last, used to create a footer.

Module 7:  File Systems

*   ln – link file

    *   -s – symbolic
*   lsblk – list block devices
*   fdisk – partition table manipulation

    *   -l – list
    *   m – menu
    *   n – new
    *   p – print current
    *   w – write
    *   q – quit
*   partprobe – inform kernel of changes
*   mkfs.ext4 – make ext4 file system

    *   -L – label
*   mount /device /dir

    *   -a – mount all automatically
    *   -o – options

        *   defaults – alias for async,auto,dev,exec,nouser,rw,suid
        *   async – Allow the asynchronous input/output operations
        *   auto  – mount automatically using mount -a
        *   noauto – no automatic mount
        *   dev   – Interpret character or block special devices on the file system
        *   exec  – allow the execution of binaries
        *   noexec – no execution of binaries
        *   nouser – disallow non-root to mount and unmount
        *   rw / ro – read/write / read-only
        *   suid  – Allow set-user/group bits to take effect.
        *   remount – Remount the file system in case it is already mounted.
*   umount – unmount
*   fstab – format:
    [device]   [directory]   [type]   [options]   [dump(0,1)]   [fsck(0,1,2)]
*   swapon --
*   parted – partition table manipulation

    *   print free
*   swapon/swapoff – control swap devices and files

    *   -s – show swap
    *   -a – all
    *   -L – label
    *   -v – verbose
*   mkswap – create swap area

    *   -L – label

*   pvcreate – create a PV
*   pvdisplay – display detailed information about a PV
*   pvremove – remove (destroy) a PV
*   pvresize – resize PV to reflect size of underlying device
*   pvs – display information about PVs on a system
*   pvscan – scan devices for LVM (PV) data; update cache

*   vgcreate – create a VG
*   vgdisplay – display detailed info about VG(s)
*   vgextend – add PV(s) to VG
*   vgreduce – remove PV(s) from VG (CAUTION!)
*   vgremove – destroy a VG
*   vgs – display information about VGs
*   vgscan – scan devices for LVM (VG) data; update cache

*   lvcreate – create an LV
*   lvdisplay – display detailed information about an LV
*   lvextend – add physical extents to an LV
*   lvreduce – remove physical extents from an LV
*   lvremove – destroy an LV
*   lvresize – shrink or grow an LV (-r autoresize resident FS)
*   lvs – display information about LVs
*   lvscan – scan devices for LVM (LV) data; update cache

*   cryptsetup

    *   luksFormat – create a LUKS device
    *   luksOpen – open LUKS for reading
    *   luksClose – close LUKS access
    *   add mapping and keys in /etc/crypttab

Module 8:  Processes and Services

*   ps – show running processes

    *   -e – everything
    *   -f – full listing
    *   -u – user
    *   -Z – selinux
*   kill – pass a signal

    *   -9 – KILL
    *   -20 – SPT (pause)
    *   -18 – CONT (resume)
*   CTL-z – pause a process

    *   fg/bg – resume foreground / background
    *   bg – resume background
    *   disown

        *   -a – all
        *   -h – leave in table, do not terminate on exit
*   nice – set a process priority

    *   -n – value (-20 to 19)
    *   renice – change a process priority
*   limit user resources in /etc/security/limits.conf

    *   ulimit – adjust limits on the fly
*   top – view running processes

    *   h – Display a help screen
    *   i – toggle idle processes
    *   f – Select fields to display
    *   F – Select sort field
    *   M – Sort by memory usage.
    *   P – Sort by CPU usage.
    *   V – Show parent process relationships
    *   u – Filter by user.
    *   r – Renice a process.
    *   k – Kill a process.
    *   q – quit top
*   free / vmstat – display memory
*   pgrep / pkill – process grep / pgrep and signal processes

    *   -u – user
    *   -l – long (shows command line)
    *   -n – newest
    *   -v – invert selection
*   killall – signal multiple processes

    *   -u – user
    *   -i – interactive (prompt)
    *   -v – verbose, not invert

Module 9:  Scheduling Events

*   at – schedule events once

    *   atq – list jobs
    *   atrm – remove jobs
    *   -c – show job script
    *   batch – schedule when cpu usage is below threshold set with at -l
*   crontab – schedule precisely

    *   -l – list
    *   -e – edit
    *   -u – user
    *   Format:
        [minute]  [hour]  [day]  [month]  [day of week]  [/path/cmd]
*   anacron – schedule roughly

    *   create link from job to /etc/cron.interval

Module 10:  Booting

*   runlevel – view previous and current runlevel
*   telinit – change runlevel

    *   0 – halt
    *   1 – Single-user
    *   3 – Multi-user
    *   5 –graphical
    *   6 – reboot
    *   default set in /etc/inittab
*   chkconfig – enable services

    *   no arguments – show all
    *   on / off – enable / disable service
    *   --list
    *   --level – set at specific runlevels
*   grub-crypt --sha-512 – generate password hash
*   touch /.autorelabel – restore selinux context on entire file system
*   shutdown, poweroff, halt, reboot

    *   -f – force

Module 11:  Logs

*   rsyslog.conf severities

    *   0emerg
    *   1alert
    *   2crit
    *   3err
    *   4warning
    *   5notice.
    *   6info
    *   7debug
    *   .none
*   logrotate.conf
*   logger -p – generate syslog message with priority
*   timezone – link from /usr/share/zoneinfo/… to /etc/localtime
*   date

    *   -s – set "DD month YYYY HH:MM:SS" or HH:MM:SS
*   ntpdate – manual ntp sync
*   ntp.conf
*   ntpq -p – ntpd status

Module 12:  SELinux

*   semanage – policycoreutils-python package

    *   login
    *   user
    *   port
    *   permissive
    *   boolean
    *   fcontext – file context
    *   -l – list
    *   -d – delete
    *   -a – add
    *   -e – set equal (requires source and target)
    *   wildcard a directory – "/web(/.*)?"
*   seinfo – setools-console package

    *   -a – attribute (no space)
    *   -x – print a list
*   getenforce / setenforce – view/change selinux status
*   sealert – setroubleshoot-server package
*   getsebool / setsebool – view/change selinux boolean

    *   -P – persistent
*   sesearch – policy query

    *   -b – boolean
    *   --rule – allow, type, neverallow, audit, dontaudit, all
    *   -s – source
    *   -t – target
    *   -c – class (file, dir, socket)
    *   -p – permission type (read, write, create)
*   ausearch – query audit logs

    *   -c – common name
    *   -i – interpret numbers to names
    *   -m – message type
    *   -ts – time start
*   restorecon – restore SELinux context on a file/directory

    *   -R – recurse
    *   -v – verbose
*   audit2allow

    *   -o – output file
*   semodule – manage SELinux policy modules

    *   -i – install
    *   -d – disable

Module 13:  Networking

*   set hostname in /etc/sysconfig/network
*   set name resolution in /etc/hosts, nsswitch, and resolv.conf
*   set ip address in /etc/sysconfig/network-scripts/ifcfg-ethX
*   ifup /ifdown – reset an interface
*   ifconfig – view interface information
*   network diagnostics – ping, traceroute, tracepath, dig, nslookup
*   netstat – show socket information

    *   -c – continuous
    *   -l – listening ports only
    *   -a – all ports
    *   -e – extended detail
    *   -t – TCP
    *   -u – UDP
    *   -p – show PID and program that owns the socket
    *   -n – numeric address only
    *   -s – statistics
*   ss – socket status

    *   -m – memory usage
    *   -o – time
    *   state – established, syn-sent, syn-recv, connected
    *   src/dst – source or destination address
    *   sport/dport – source / destination port (:443)
*   whois – query a name registrar, installed as the jwhois package
*   curl / wget – non-interactive ways to download from a URL
*   tcpdump – wire-level level listener/parser

*   iptables – manage the firewall

    *   -L – list
    *   -v – verbose
    *   --line-numbers
    *   -I – insert a rule
    *   -A – append
    *   -D – delete
    *   -R – replace
    *   -F – flush all
    *   -p – protocol
    *   --dport – destination port
    *   -j – jump to target
    *   --policy – set default policy (DROP)
    *   -m – match (state)

        *   --state – RELATED, ESTABLISHED, NEW
*   service iptables…

    *   status – show all rules
    *   save – save running config to /etc/sysconfig/iptables

Module 14:  Installing Software

*   yum

    *   repolist – shows repos in /etc/yum.repos.d/
    *   repoquery
    *   list installed
    *   search
    *   info
    *   provides – what package provides a binary
    *   clean all – clear caches
    *   makecache
*   createrepo – build repository metadata
*   rpm

    *   --import – import GPG key
    *   -Va – verify all
    *   -q – query

        *   f – file (shows parent package)
        *   c – configuration files
        *   l – list all installed by package
    *   -i – install
    *   -U – upgrade

Module 15:  Remote File Systems

*   nfs – part of nfs-utils package
*   edit /etc/exports format:
    [local share] [hostname or network] [options]

    *   options include:

        *   rw –read/write
        *   sec= –security flavors (sys, krb5, krb5i, krb5p)
        *   sync – do not reply until write
        *   fsid=0 – sets the “root” of the virtual file system in NFSv4
        *   anonuid – set the system UID to be assigned to anonymous users
        *   no_root_squash – do not map UID 0 requests to anonymous
*   exportfs – re-read /etc/exports

    *   -a – all
    *   -u – unexport

*   vsftpd – configured in vsftpd.conf

    *   requires IPTABLES MODULES="ip conntrack ftp" in iptables-config
    *   lftpd – ftp client

*   httpd – configured in httpd.conf

    *   curl, wget, lynx – clients for url-based targets

Module 16:  Remote Access

*   vnc – tigervnc and tigervnc-server packages

    *   uses ports 5800,5900,6000 – increment by one for each additional user
    *   vncpasswd – set password (after su -)
    *   start manually with vncserver :display number
    *   start automatically by configuring /etc/sysconfig/vncservers
*   vncviewer user@host  host:number  -- connect to vnc server

*   sshd – configured in /etc/ssh/sshd_config
*   ssh user@host

    *   -i – identity file (key)
*   ssh-keygen – make key
*   ssh-copy-id – copy key to remote host
*   scp localfile  user@host:/path/file – copy localfile to remote host
*   sftp – ftp client over ssh

Module 17:  Kernel Modules and Parameters

*   lsmod – list kernel modules
*   modinfo – provide information about a module
*   modprobe – add / remove modules from the kernel

    *   reads files (options and blacklists) from /etc/modprobe.d/
    *   -l – list
    *   -r – remove
    *   -c – show configuration
*   sysctl – alter kernel parameters

    *   -a – display all
    *   -w – write active parameter
    *   persistent settings in sysctl.conf

Module 18:  Disaster Recovery

*   dd if=infile of=outfile – copy data

    *   conv=noerror – ignore read errors
    *   bs= – block size
    *   count= – number
*   shred – securely delete
*   tar – archiving

    *   -c – create
    *   -z – zip
    *   -p – preserve permissions
    *   -t – list contents of archive
    *   -v – verbose
    *   -x – extract
    *   -C – change directory
    *   -d – find differences between archive and file system
    *   -f – archive filename follows
    *   --xattrs – preserve both SELinux and acls attributes, use when creating and extracting
*   rsync – remote syncronization

    *   -a – archive, equivalent to -rlptgoD:  recurse, copy links; save permissions, timestamps, group, and owner; also preserve Device and special files.
    *   -v – verbose
    *   -e – use specified transport, such as "ssh -i /path/key"
    *   -X – preserve extended attributes
    *   -A – preserve ACLs
    *   -S – squeeze sparse files (those with long zero blocks)
    *   -L – turn links into files
    *   --delete – remove files not at the source, default is to preserve them at the destination
    *   --remove-source-files – delete source upon success, useful for temporary tarballs
    *   --include / --exclude / --filter – allows detailed specification of files
*   rear mkbackup – relax and recover

Module 19:  Security

*   aide – detect file system changes

    *   fix hash types and exclude active files in aide.conf
    *   -i – create initial database

        *   remove .new from the name
    *   -C – compare (outputs to /var/log/aide/aide.log)
    *   -u – update the database
*   git – stupid content tracker

    *   clone – a repository to a local directory