
```bash
# find -perm looks at the permissions of the file: 4000 and above
# are setuid/setgid.

find / -type f -perm +4000 -print0 | while read -d '' -r match
do
  if [ -x "$match" ] ; then
    # Let's split file owner and permissions from the ls -ld output.
    owner="$(ls -ld $match | awk '{print $3}')"
    perms="$(ls -ld $match | cut -c5-10 | grep 'w')"
    if [ ! -z $perms ] ; then
      echo "*** $match (writable and setuid $owner)"
    elif [ ! -z $(find $match -mtime -$mtime -print) ] ; then
      echo "*** $match (modified within $mtime days and setuid $owner)"
    elif [ $verbose -eq 1 ] ; then
      # By default, only dangerous scripts are listed. If verbose, show all.
      lastmod="$(ls -ld $match | awk '{print $6, $7, $8}')"
      echo "  $match (setuid $owner, last modified $lastmod)"
    fi
  fi
done

exit 0
```

Listing 6-1: The findsuid script

### How It Works

This script checks all setuid commands on the system to see whether they're group or world writable and whether they've been modified in the last $mtime days. To accomplish this, we use the find command with arguments specifying the types of permissions on files to search for. If the user requests verbose output, every script with setuid permissions will be listed, regardless of read/write permission and modification date.

### Running the Script

This script has one optional argument: -v produces verbose output that lists every setuid program encountered by the script. This script should be run as root, but can be run as any user since everyone should have basic access to the key directories.

### The Results

We've dropped a vulnerable script somewhere in the system. Let's see if findsuid can find it in Listing 6-2.

```text
$ findsuid
*** /var/tmp/.sneaky/editme (writable and setuid root)
```

Listing 6-2: Running the findsuid shell script and finding a backdoor shell script

There it is (Listing 6-3)!

```text
$ ls -l /var/tmp/.sneaky/editme
-rwsrwxrwx 1 root wheel 25988 Jul 13 11:50 /var/tmp/.sneaky/editme
```

Listing 6-3: The ls output of the backdoor, showing an s in the permissions, which means it is setuid

That's a huge hole just waiting for someone to exploit. Glad we found it!

## #46 Setting the System Date

Conciseness is at the heart of Linux and its Unix predecessors and has affected Linux's evolution dramatically. But there are some areas where this succinctness can drive a sysadmin batty. One of the most common annoyances is the format required for resetting the system date, as shown by the date command:

```text
usage: date [[[CC]YY]MM]DD[hh:mm[.ss]]
```

Trying to figure out all the square brackets can be baffling, without even talking about what you do or don't need to specify. We'll explain: you can enter just minutes; or minutes and seconds; or hours, minutes, and seconds; or the month plus all that—or you can add the year and even the century. Yeah, crazy! Instead of trying to figure that out, use a shell script like the one in Listing 6-4, which prompts for each relevant field and then builds the compressed date string. It's a sure sanity saver.

### The Code

```bash
#!/bin/bash
# setdate - Friendly frontend to the date command
# Date wants: [[[CC]YY]MM]DD[hh:mm[.ss]]

# To make things user-friendly, this function prompts for a specific date
#   value, displaying the default in [] based on the current date and time.

. library.sh  # Source our library of bash functions to get echon().
```

This is one of the subtle problems with working with the date command. With this script, if you specify the exact time during the prompts but then have to enter a sudo password, you could end up setting the system time to a few seconds in the past. It's probably not a problem, but this is one reason why network-connected systems should be working with Network Time Protocol (NTP) utilities to synchronize their system against an official timekeeping server. You can start down the path of network time synchronization by reading up on timed(8) on your Linux or Unix system.

### Running the Script

Notice that this script uses the sudo command to run the actual date reset as shown in Listing 6-5. By entering an incorrect password to sudo, you can experiment with this script without worrying about any strange results.

### The Results

```text
$ setdate
year [2017] :
month [05] :
day [07] :
hour [16] : 14
minute [53] : 50

Setting date to 201705071450. You might need to enter your sudo password:

password $
```

## #47 Killing Processes by Name

Linux and some Unices have a helpful command called killall, which allows you to kill all running applications that match a specified pattern. It can be quite useful when you want to kill nine mighty daemons, or even just to send a SIGHUP signal to xinetd to prompt it to reread its configuration file. Systems that don't have killall can emulate it in a shell script built around ps for identification of matching processes and kill to send the specified signal.

The trickiest part of the script is that the output format from ps varies significantly from OS to OS. For example, consider how differently FreeBSD, Red Hat Linux, and OS X show running processes in the default ps output.

First take a look at the output of FreeBSD:

```text
BSD $ ps
PID TT STAT TIME COMMAND
792 0 Ss 0:00.02 -sh (sh)
4468 0 R+ 0:00.01 ps
```
