
# Search Wikipedia from the Command Line

If you need to quickly look up some information on a subject, you can search wikipedia using DNS. The name server returns wikipedia article summaries as TXT records.

```
$ dig +short txt <string>.wp.dg.cx
$ host -t txt <string>.wp.dg.cx
```

```
$ dig +short txt linux.wp.dg.cx
"Linux is a Unix-like computer operating system
assembled under the model of free and open source
software development and distribution. The defining
component of Linux is the Linux kernel, an operating
system kernel first released 5 October 1991 by Linus
Torvalds. http://en.wikipedia.org/wiki/Linux"
$ host -t txt bash_shell.wp.dg.cx
bash_shell.wp.dg.cx descriptive text "Bash is a Unix
shell written by Brian Fox for the GNU Project as a free software replacement for the Bourne shell (sh). Bash is a command processor, typically run in a text window, allowing the user to type commands which cause actions. Bash can also read commands from a file, called a script. Like all Unix shells, it supports filename wildcarding, piping, here documents...
http://en.wikipedia.org/wiki/Bash_(Unix_shell)"
```

You can create a small shell script to save yourself from typing the full DNS query each time.

```
$ echo -e '#!/bin/bash\ndig +short txt ${1}.wp.dg.cx' > wikidig

$ chmod 755 !$
chmod 755 wikidig

$ ./wikidig ubuntu_operating_system
"Ubuntu As of 2012, according to online surveys, Ubuntu is the most popular Linux distribution on desktop/laptop personal computers, and most Ubuntu coverage focuses on its use in that market. However, it is also popular on servers and for cloud computing.
http://en.wikipedia.org/wiki/Ubuntu_(operating_system)"
```

Alternatively, you could create a function instead and add it to your dot files.

```
$ echo 'wikidig(){ dig +short txt ${1}.wp.dg.cx; }' >> .bash_profile
$ . ./.bash_profile
```

```
$ wikidig jazz
"Jazz is a musical style that originated at the beginning of the 20th century in black communities in the Southern United States. It was born out of a mix of African and European music traditions. Its African pedigree is evident in its use of blue notes, improvisation, polyrhythms, syncopation and the swung note. From its early development until the present day jazz has also…
http://en.wikipedia.org/wiki/Jazz"
```

# Make Non-Interactive Shell Sessions Behave the Same as Interactive Sessions

Make any customizations in `~/bashrc`. The contents of `~/bash_profile`:

```
if [ -f ~/.bashrc ]; then
source ~/.bashrc
fi
```

The shell behaves in slightly different ways when you log on interactively versus when you just connect to run a single command. The contents of .profile or .bash_profile are only executed for interactive sessions. If you are not aware of this subtle difference it may leave you scratching your head as to why something works perfectly when you log in and execute a command versus when you just ssh in to run that same command. You can save yourself some hassle by making your interactive and non-interactive sessions behave the same. To do this, configure .bash_profile to reference .bashrc and put all of your configuration in .bashrc.

Here is an example to better illustrate the difference between interactive and non-interactive shells. For example, if you define an alias for ll in `~/bash_profile` it will work during an interactive session but it will not be available during a non-interactive session.

### Interactive

```
mac:~ jason $ ssh linuxserver
jason@linuxserver:~$ uptime
    11:49:16 up  97 days,  2:59,   5 users,  load average:
    0.15, 0.25, 0.31
jason@linuxserver:~$ ll
-rw-r--r-- 1 jason jason 221 Nov 13 11:30 file.txt
jason@linuxserver:~$ exit
logout
Connection to 10.0.1.9 closed.
mac:~ jason $
```

### Non-Interactive

```
mac:~ jason$ ssh linuxserver uptime
    11:49:16 up 97 days, 2:59, 5 users, load average:
    0.15, 0.25, 0.31
mac:~ jason$ ssh linuxserver ll
bash: ll: command not found
mac:~ jason$
```

```
$ cat .bash_profile
# Put our settings in .bashrc so we have the same
environment for login and non-login shells.
if [ -f ~/.bashrc ]; then
    source ~/.bashrc
fi
```

```
$ cat .bashrc
alias ll='ls -l'
HISTFILESIZE=5000
export HISTFILESIZE
```

# Make Your Computer Talk to You

```
$ espeak -f file
$ echo text | espeak
```

Espeak converts text to speech. You can provide espeak a file or pipe in text for it to speak. If you have a long running task you can let your computer tell you when it's finished as in this example.

```
$ for VIDEO in $(ls *.mp4 | sed 's/\.mp4//')
> do
>         avconv -v quiet -i $VIDEO.mp4 $VIDEO.mp3
> done; echo "File conversions complete." | espeak
```

# Display the Current Date and Time in a Different Time Zone

```
$ TZ=<TIMEZONE> date
```

The TZ environment variable specifies the time zone. If you want to know the time in a given time zone, prepend the environment variable and time zone to the date command.

```
$ TZ=America/Los_Angeles date
Sun Apr  6 19:37:46 PDT 2014
$ TZ=MST date
Sun Apr  6 19:37:48 MST 2014
$ TZ=CST date
Mon Apr  7 02:37:50 CST 2014
$ TZ=UTC date
Mon Apr  7 02:37:53 UTC 2014
```

It's a common practice to use UTC as the time zone on servers. If your workstation or laptop is set to a different time zone, you can create an alias that quickly gives you the time in UTC.

```
$ alias utc='TZ=UTC date'
$ utc
Mon Apr  7 02:35:01 UTC 2014
```

# Display a Calendar at the Command Line

```
$ cal
$ cal MM YYYY
$ cal YYYY
```

To display a calendar at the command line use the cal command. Use the -3 option to display the previous, current, and next month. If you want to see the calendar for a specific month use MM YYYY or for an entire year use YYYY.

```
$ cal

     April 2014
Su Mo Tu We Th Fr Sa
             1  2  3  4  5
 6  7  8  9 10 11 12
13 14 15 16 17 18 19
20 21 22 23 24 25 26
27 28 29 30
```

```
$ cal -3

    March 2014         April 2014          May 2014
Su Mo Tu We Th Fr Sa Su Mo Tu We Th Fr Sa Su Mo Tu We Th Fr Sa
                                1  2  3  4  5               1  2  3
 2  3  4  5  6  7  8    6  7  8  9 10 11 12   4  5  6  7  8  9 10
 9 10 11 12 13 14 15   13 14 15 16 17 18 19  11 12 13 14 15 16 17
16 17 18 19 20 21 22   20 21 22 23 24 25 26  18 19 20 21 22 23 24
23 24 25 26 27 28 29   27 28 29 30           25 26 27 28 29 30 31
30 31
```

```
$ cal 10 2014

    October 2014
Su Mo Tu We Th Fr Sa
             1  2  3  4
 5  6  7  8  9 10 11
12 13 14 15 16 17 18
19 20 21 22 23 24 25
26 27 28 29 30 31
```

# Extract a Tar Archive to a Different Directory

```
$ tar xf tarfile.tar -C /path/to/directory
```

Instead of changing directories and untarring a file, you can use the -C option.

```
$ tar xf projectfiles.tar -C /usr/local/myproject
```

This is equivalent to these two commands.

```
$ cd /usr/local/myproject
$ tar xf ~/projectfiles.tar
```

# Transform the Directory Structure of a Tar File When Extracting It

```
$ tar xf tarfile.tar --strip-components=NUMBER
```

If you want to extract a tar file starting at a subdirectory, use the --strip-components option. For example, if you download a release from github.com the name and version of the project is the top directory in the tar file. To extract the files below that directory use --strip-components=1.

```
$ curl -sLO https://github.com/twbs/bootstrap/archive/v3.1.1.tar.gz
$ tar ztvf v3.1.1.tar.gz | head -1
drwxrwxr-x root/root     0 2014-02-13 12:24 bootstrap-3.1.1/
$ tar zxfv v3.1.1.tar.gz --strip-components=1 -C ~/bootstrap-latest
$ ls -1 ~/bootstrap-latest
bower.json
```
