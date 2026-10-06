
```
root@kemal:/usr/share/doc# ls
trace
acceck
accountservice
ace-voip
ac
adduser
adwaita-icon-theme
afflib-tools
agfln
aircraft-ng
alsa-tools
amap
amd64-microcode libpng12-dev
libpod-latex-perl
libpod-readme-perl
polkit-agent-1-0
libpolkit-backend-1-0
libpolkit-geoip-1-0
libpopler-46
libpopler-glib
libpopler-qt4-4
libport0
libportaudio2
libpostproc52
libpotrace0
```

Man pages are the basic help files in the linux system. A man page structure is usually like this:

- NAME: Command's name and definition
- SYNOPSIS: how to use the command
- DESCRIPTION: Description of the function of the command
- EXAMPLES: Examples of how to use the command.
- SEE ALSO: Related titles.

Manual pages located below, /usr/share/man.

```
root@kemal:/usr/share/man# ls id man1 man5 nl pt_BR sl vi
cs es fr.,UTF-8 gl it man2 man6 pl ro sr zh
da fi qi ja man3 man7 pl.UTF-8 ru sv_CN
de br hr de.UTF-8 fr.TR.ISO8859-1 hu ko man4 man8 pl sk tr zh_TW
root@kemal:/usr/share/man# _
```

Configuring the manual pages as follows:

- man1: General user programs.
- man2: System programs.
- man3: Library functions. (About C programming)
- man4: Private files.
- man5: File formats.
- man6: Games and screensavers.
- man7: Various commands which do not fit into the other categories.
- man8: System administration and maintenance.

To view the man help page for the ls command, (explaining help command that we give an example above) we can use **man ls command**.

![](img/aa6ce54dbb8ffe5b9d7befb8c6764064_28_0.png)

After reviewing the help topics in the manual pages, to exit we should pres **Q** key.

# 30 | Master of Linux Commands

## Whatis

There is another command **whatis** command, which helps us indirectly. We can use this command to find out where the help topic of an application or command in the manual.

```
root@kemal:~ whatis echo
echo (1)           - display a line of text
```

If you want to make queries using wildcards that we will talk about later, you must use the **-w** parameter. For example **whatis -w cal**.

```
root@kemal:~ whatis cal+
cal+: nothing appropriate.
root@kemal:~ whatis cal+
cal (1)           - displays a calendar and the date of Easter
calendar (1)      - reminder service
calloc (3)       - allocate and free dynamic memory
calloc (3avr)     - (unknown subject)
callprpc (3)     - library routines for remote procedure calls
```

## Apropos

**apropos** command which is to be used to get help actually runs **man -k** command in the background.

```
root@kemal:~ man -k printf
asprintf (3)      - print to allocated string
dnprintf (3)       - print to a file descriptor
fprintf (3)       - formatted output conversion
printf (3avr)     - (unknown subject)
printf.P (3avr)   - (unknown subject)
fprintf (3)      - formatted character output conversion
printf (1)        - format and print data
printf (3)        - formatted output conversion
printf (3avr)     - (unknown subject)
printf.P (3)       - (unknown subject)
sprintf (3)      - formatted output conversion
sprintf (3avr)     - (unknown subject)
sprintf.P (3avr)   - (unknown subject)
```

Looking at the output command we see the applications including **printf** term are listed. The output of the **apropos** command will be the same as output of **man -k** command.

```
root@kemal:~# apropos printf
asprint - to allocated string
dprintf (3) - print to a file descriptor
printf (3) - formatted output conversion
printf (3avr) - (unknown subject)
printf P (3avr) - (unknown subject)
fwprintf (3) - formatted wide-character output conversion
printf (1) - format and print data
printf (3) - formatted output conversion
printf (3avr) - (unknown subject)
```

Finally, if we cannot find the help in the man page, we can try after we update the man directory memory. Mandb can be used for the update command.

```
root@kemal:~# mandb
Purging old database entries in /usr/man...
Processing manual pages under /usr/man...
Purging old database entries in /usr/share/man...
Processing manual pages under /usr/share/man...
Purging old database entries in /usr/share/man/zh...
Processing manual pages under /usr/share/man/zh...
Purging old database entries in /usr/share/man/sr...
```

# Chapter 3: Commands to Get Information

There are several commands to get the relevant information stored in our system about processes, users, etc.

### Lsb Release

To find out the Linux distribution name that we have, we use lsb_release -a.

```
root@kemal:-# lsb_release -a
No LSB modules available.
Distributor ID: Kali
Description: Kali/Linux 2.0
Release: 2.0
Codename: Kali
```

A similar command is cat /etc/release. With this we can get little more information about our system.

```
root@kemal:-# cat /etc/release
DISTRIB_ID=Kali
DISTRIB_RELEASE=2.0
DISTRIB_DENAME=Kali
PRETTY_NAME="Kali/Linux 2.0"
NAME="Kali"
VERSION="2.0"
ID_LIKE=debian
HOME_URL="http://kali.org/"
SUPPORT_URL="http://forums.kali.org/"
BUG_REPORT_URL="http://bugs.kali.org/"
```

# 34 | Master of Linux Commands

### Issue

To see linux name that we are using, cat /etc/issue commands also be used.

```
root@kemal:~# cat /etc/issue
Kali/Linux 2.0
```

### uname

To find out the kernel version of our system, uname -a command can also be used.

```
root@kemal:~# uname -a
Linux kemal 4.0.0-kali1-686 #1 SMP Debian 4.0.4-1+kali (2015-06-03) i686
```

In fact, with -a parameter we did not only learn kernel version, we also learn kernel name, all the information, such as architecture. Individual query can be done as the following.

```
root@kemal:~# uname
Linux
root@kemal:~# uname -n
kemal
root@kemal:~# uname -m
i686
root@kemal:~# uname -r
4.0.0-kali1-686
```

### Cal

We can use the cal command to display the system on the console as a monthly calendar of the month we were in.

```
root@kemal:~# cal
Agustos 2015
Pe Sa Pr Cu
             1
2 3 4 5 6 7 8
9 10 11 12 13 14 15
16 17 18 19 20 21 22
23 24 25 26 27 28 29
30 31
```

For example, if you want to see first month of 1977, you should use the command as cal 1 1977.

```
root@kemal:~# cal 1 1977
Ocak 1977
Pe Sa Pr Cu
             1
2 3 4 5 6 7 8
9 10 11 12 13 14 15
16 17 18 19 20 21 22
23 24 25 26 27 28 29
30 31
```

For a specific year, we can use a command similar to the following.

### Date

Date command is used to find the current time and date information of the system.

```
root@kemal:~# date
Sat Aug 22 21:00:34 EEST 2015
```

### Hostname

To view the hostname we get from the computer system that we use, we can use the hostname command.

```
root@kemal:~# hostname
kemal
```

## Who-Whoami

To find out who is active in the system, who's been login, to find an identity information, we can use w, who, whoami commands.

```
root@kemal:-# w
01:55:59 up 8:17, 2 users, load average: 0.78, 1.06,
USER     TTY             FROM LOGIN@ IDLE JCPU
root     :0               0               17:39 ?xdm? 55:50
root     pts/0           :0               17:48 0.00s 0.58
```

There are uses of these commands. Briefly:

- w: To find out the information which user runs at that moment which applications / command.
- who: Identity which profile is worked in the system.
- whoami: Identify which profile user is working with.

```
root@kemal:-# who              2015-08-22 17:39 (:0)
root     :0
root     pts/0         2015-08-22 17:48 (:0)
root@kemal:-# whoami
root
root@kemal:-# am i
root     pts/0         2015-08-22 17:48 (:0)
```

When we use who command with -b we can see when the system run last time, with -r shows the opening levels (runlevel).
