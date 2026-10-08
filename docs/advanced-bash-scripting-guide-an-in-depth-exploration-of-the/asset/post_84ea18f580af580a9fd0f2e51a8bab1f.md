
# Advanced Bash-Scripting Guide

wall

This is an acronym for "write", i.e., sending a message to all users at every terminal logged into the network. It is primarily a system administrator’s tool, useful, for example, when warning everyone that the system will shortly go down to a problem (see Example 19-1).

```bash
$ wall "System going down for maintenance in 5 minutes!"
Broadcast message from bozo (pts/1) Sun Jul 8 13:53:27 2001...
System going down for maintenance in 5 minutes!
```

If access to a particular terminal has been disabled by me, then wall cannot send a message to that terminal.

## Information and Statistics

uname

Output system specifications (OS, kernel version, etc.) to stdout. Invoked with the -a option, gives verbose system info (see Example 16-5). The -s option shows only the OS type.

```bash
$ uname
Linux

$ uname -s
Linux

$ uname -a
Linux iron.iron 2.6.15-2054_FC5 #1 Tue Mar 14 15:48:33 EST 2006 1686 1686 1386 GNU/Linux
```

arch

Show system architecture. Equivalent to uname -m. See Example 11-27.

```bash
$ arch
1686

$ uname -m
1686
```

lastcomm

Gives information about previous commands, as stored in the /var/account/pacct file. Command name and user name can be specified by options. This is one of the GNU accounting utilities.

lastlog

List the last login time of all users. This references the /var/log/lastlog file.

```bash
$ lastlog
root              tty       Fri Dec 7 18:43:21 -0700 2001
bin               **Never logged in**
daemon            **Never logged in**
...
bozo              tty       Sat Dec 8 21:14:29 -0700 2001
```

lsof

List open files. This command outputs a detailed table of all open files and gives information about their owner, size, and more. lsof may be piped to grep or awk to analyze results. The lsof command is useful, complex administrative tool. If you are unable to determine which files are still open on filesystem, then lsof helps trace intrusion or attacks. The -i option lists network socket files.

| COMMAND | USER | FD | TYPE | SIZE | NAME |
| :--- | :--- | :--- | :--- | :--- | :--- |
| init | root | 1,5 | REG | 30748 | /sbin/init |
| init | root | 1,5 | REG | 73120 | /lib/libc.so.3.so |
| init | root | 1,5 | REG | 93168 | /lib/ld-linux.so.so |
| cdmgr | root | 1,5 | REG | 36956 | /sbin/cdmgr |
| firefox | bozo | 32u | ipv4 | 9956 | 66.0.118.137:5796
| firefox | bozo | 38u | ipv4 | 10535 | 66.0.118.137:5770 |

strace

System debugging for tracing system calls and signals. And strace is useful for diagnosing why a program fails to run perhaps due to missing libraries or related cases.

```bash
$ strace df
execve("/bin/df", ["df"], /* args */) = 0
uname(sys="Linux", node="bozo.localdomain", ...) = 0
brk(0) = 0
```

ltrace

Library tracing and debugging tool that traces libraries called by a given command. This is the Linux equivalent of Solaris truss.

```bash
$ ltrace df
__libc_start_main(0x804a910, 1, 0xbf5894a, 0x80fb70, 0x<unfinished>) = 0
setlocale(6, "*") = "en_US.UTF-8"
bindtextdomain("coreutils", "/usr/share/locale") = "/usr/share/locale"
textdomain("coreutils") = "coreutils"
__cxa_atexit(0x804b650, 0, 0, 0xbf58bf90) = 0
getenv("DF_BLOCK_SIZE") = NULL
```

nc (netcat) utility is a complete toolkit for connecting to and listening to TCP and UDP ports. It is useful as diagnostic and testing tool and as a simple script-based HTTP client and.

```bash
$ nc localhost.localdomain 25
220 localhost.localdomain ESMTP Sendmail 8.13.1/8.13.1;
Thu, 31 Mar 2005 15:41:35 -0700
```

### Example 17-5. Connecting a remote server for ident

```bash
#!/bin/sh
## Duplicate Dave's ident-scan thingie using netcat. Oooh, he'll be pissed.
## Args: target port [port ...]
## Use stdout and stderr together.

## Advantages: slower than ident-scan, giving inetd less for alarm, and only hits the few daemon ports you specify.
## Disadvantages: requires numeric-only args, the output sleek, and won't work for r-services when coming from high source ports.
## Script author: Hobbit ~hobbit@avian.org~
## Used in ABS Guide with permission.

E_BADARGS=6      # Need at least two args.
TWO_WINKS=3       # How long to sleep.
THREE_WINKS=3
# Authentication "tap ident" port.
IDPORT=113
RAND1=999
RAND2=31337
TIMEOUT0=0
TIMEOUT1=8
TIMEOUT2=4

case "${2}" in
  "") echo Need HOST and at least one PORT."; exit E_BADARGS ;;
esac

# Ping once and see if they are running ident.
if nc -z -w $TIMEOUT0 "$1" "$IDPORT" >/dev/null 2>&1; then
  echo "$1 is running ident."
else
  echo "oops, $1 isnt running ident."
  exit 0
fi

# Generate a randomish port.
PORT=$(expr $RAND1 + $RAND2)

# How long to connect.
while true; do
  nc -v -w $TIMEOUT1 "$1" "$PORT" >/dev/null 2>&1; then
    break
  fi
  sleep $THREE_WINKS
done
```

du

Show (disk) file usage, recursively. Defaults to current working directory, unless otherwise specified.

```bash
$ du -ach
1.0k /wi.sh
1.0k /tst.sh
1.0k /random.file
6.0k
6.0k total
```

free

shows memory and cache usage in tabular form. The output shows free, and much more.

```bash
$ free
Mem: 30504 28624 15820 1608 16376
buffers/cache: 10640 19864 5412
Swap: 68540 3128 65412
```

df

Shows files usage in tabular form.

| Filesystem | 1-blocks | Used | Available | % | Mounted on |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/hda5 | 273262 | 92607 | 166547 | 36% | / |
| /dev/hda8 | 222525 | 123951 | 87085 | 59% | /home |
| /dev/hda7 | 140896 | 107574 | 261488 | 80% | /usr |

dmesag

Lists all system boot messages to stdout. Handy for debugging and ascertaining which device drivers were installed and system interrupts in them. The output of dmesag, of course, be parsed with grep, sed, or awk within a script.

```bash
$ dmesag | grep /dev/hda2
Kernel command line: root=/dev/hda2
hda: IBM-DLGA-23080, ATA DISK drive
hda: 601574 sectors (308 MB) W/96KB Cache, Csh=746/128/63
hda hda2 hda3 < hda5 hda7 > hda4
```

lsdev

List devices, is installed hardware.

| Device | I/O Ports | IRQ |
| :--- | :--- | :--- |
| cascade | 4 | 080 |
| dma | 0000 | 01f |
| dml1 | 00c | 0df |
| dma2 | 000f | ff |
| ide0 | 14 | 1f7 |

procinfo

Extract list and information from the /proc pseudo-filesystem. This gives a very extensive and detailed listing.

```bash
$ procinfo | grep Bootup
Bootup: Wed Mar 21 15:15:50 2001 Load average: 0.04 0.21 0.34 1/47 .829
```

stat

Gives detailed and verbose statistics on a given file (or a directory file) or set of files. If the target file does not exist, stat returns an error message.

```bash
$ stat nonexistent-file
nonexistent-file: No such file or directory
```

In a script, you can use stat to extract information about files (and filesystems) and variables accordingly.

```bash
#!/bin/bash
# fileinfo2.sh

# Per suggestion of Joël Bourquard and . . .
# http://www.linuxquestions.org/questions/showthread.php?t=410766
```

FILENAME=testfile.txt
