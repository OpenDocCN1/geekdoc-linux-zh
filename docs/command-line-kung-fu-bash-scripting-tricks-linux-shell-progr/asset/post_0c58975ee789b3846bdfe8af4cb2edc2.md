
## Table of Contents (Continued)

- Execute a Command at a given Time . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 95
- Share Your Screen Session with Another User . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 96
- Execute an Unaliased Version of an Aliased Command . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 98
- Save the Output of a Command as an Image . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 98
- About the Author . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 100
- Other Books by the Author . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 101
- Courses by the Author . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 102
- Index . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 103
- Appendix . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 114
- Trademarks . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 114

## Your Free Gift

As a thank you for reading *Command Line Kung Fu*, I would like to give you a copy of *Linux Alternatives to Windows Applications*. In it, you will be introduced to over 50 of the most popular applications available for Linux today. These applications will allow you to browse the web, watch movies, listen to music, connect to your favorite social networks, create presentations, and more. This gift is a perfect complement to this book and will help you along your Linux journey. Visit [http://www.linuxtrainingacademy.com/linux-apps](http://www.linuxtrainingacademy.com/linux-apps) to download your free gift.

## Introduction

I have been working at the command line on Unix and Linux systems since the 1990's. Needless to say, I feel right at home with nothing more than a dollar sign and a flashing cursor staring at me. Over the years I've picked up several command line "tricks" that have saved me time and frustration.

Some of these tips were born out of necessity — I simply had too much work to complete and too little time to do it in. Others were modeled after popular patterns found in computer programming and application development. The rest were shared with me, either directly or indirectly, by my command line heroes and mentors. It's amazing what you can learn by watching, emulating, and taking advice from a seasoned Unix and Linux professional.

Even though the title is Command Line Kung Fu, you don't have to be a Linux ninja to use the tactics presented in this book. The tips work as presented. You can start putting them to use immediately without fully understanding all the details and nuances. However, if you want or need more information, explanations and practical real-world examples follow each one.

Also, if you want to see some of these commands in action visit [http://www.linuxtrainingacademy.com/fu](http://www.linuxtrainingacademy.com/fu). There you will find a series of videos that demonstrate some of the commands covered in this book.

Finally, if you want an overview of the Linux command line and operating system please read my other book *Linux for Beginners*. It will give you a strong foundation upon which you can build your Linux skills.

Let's get started.

## Shell History

### Run the Last Command as Root

```bash
$ sudo !!
$ su -c "!!"
```

If you ever forget to run a command with root privileges, you can simply repeat it by using `sudo !!` or `su -c "!!"`.

```bash
$ adduser sam
-bash: /usr/sbin/adduser: Permission denied
$ sudo !!
sudo: adduser sam
$ id sam
uid=1007(sam) gid=1007(sam) groups=1007(sam)
$ userdel -r sam
-bash: /usr/sbin/userdel: Permission denied
$ sudo !!
sudo userdel -r sam
$ id sam
id: sam: No such user
$ useradd jim
-bash: /usr/sbin/useradd: Permission denied
$ su -c "!!!"
su -c "useradd jim"
Password:
$ id jim
uid=1007(jim) gid=1007(jim) groups=1007(jim)
```

This exclamation mark syntax is called an event designator. An event designator references a command in your shell history. Bang-Bang (!!) repeats the most recent command, but one of my favorite uses of the event designator is to run the most recent command that starts with a given string. Here's an example.

```bash
$ whoami
jason
$ uptime
12:33:15 up 35 min, 1 user, load average: 0.00, 0.00, 0.00
$ df -hT /boot
Filesystem Type Size Used Avail Use% Mounted on
/dev/vda1 ext4 485M 55M 406M 12% /boot
$ !u
uptime
12:33:29 up 35 min, 1 user, load average: 0.00, 0.00, 0.00
$ sudo !w
sudo whoami
root
```

### Repeat the Last Command That Started with a Given String

```bash
$ !<string>
```

This is another example of an event designator. To recall the most recent command that begins with `<string>`, run `!<string>`. You can simply specify the first letter, or as much of the string to make it unique. This example demonstrates that concept.

```bash
$ who
jason    pts/1    2014-04-06 21:04 (192.168.1.117)
$ w
jason    pts/1    192.168.1.117 21:04 0.00s
0.33s 0.00s w
$ !w
w
jason    pts/1    192.168.1.117 21:04 0.00s
0.33s 0.00s w
$ !wh
who
jason    pts/1    2014-04-06 21:04 (192.168.1.117)
```

Here is a practical example where you check to see if a process is running, kill it, and confirm that it did indeed stop.

```bash
$ ps -fu apache
UID  PID  PPID C STIME TTY TIME CMD
apache 1877 1879 0 21:32 ? 00:00:00
/usr/sbin/httpd
apache 1879 1 0 21:32 ? 00:00:00
/usr/sbin/httpd
$ sudo service httpd stop
Stopping httpd: [ OK ]
$ !fp
ps -fu apache
UID PID PPID C STIME TTY TIME CMD
$
```

### Reuse the Second Word (First Argument) from the Previous Command

```bash
$ !^
```

If you need to grab the second word from the previous command, you can use the "!^" word designator. Wherever you use "!^" it will be replaced by the second word from the previous command. You can also think of this as the first argument to the previous command.

```bash
$ host www.google.com 8.8.8.8
Using domain server:
Name: 8.8.8.8
Address: 8.8.8.8#53
Aliases:
www.google.com has address 173.194.46.83
www.google.com has address 173.194.46.81
www.google.com has address 173.194.46.84
www.google.com has address 173.194.46.82
www.google.com has address 173.194.46.80

www.google.com has IPv6 address
2607:f8b0:4009:805::1013

$ ping -cl !^
ping -cl www.google.com
PING www.google.com (173.194.46.80) 56(84) bytes of data.
64 bytes from ord08s11-in-f16.l.google.net
(173.194.46.80): icmp_seq=1 ttl=51 time=17.0 ms
--- www.google.com ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 49ms

rtt min/avg/max/mdev = 17.071/17.071/17.071/0.000 ms
$
```

### Reuse the Last Word (Last Argument) from the Previous Command

```bash
$ !$
```

Quite often I find myself needing to perform another operation on the last item on the previous command line. To access that item in your current command, use '!$'.

```bash
$ unzip tpstreport.zip
Archive: tpstreport.zip
inflating: cover-sheet.doc
$ rm !$
rm tpstreport.zip
$ mv cover-sheet.doc reports/
$ du -sh !$
du -sh reports/*
4.7G  reports/
$
```

### Reuse the Nth Word from a Previous Command

```bash
$ !!!:N
$ <event_designator>:<number>
```

To access a word in the previous command use `!!:N` where N is the number of the word you wish to retrieve. The first word is 0, the second word is 1, etc. You can think of 0 as being the command, 1 as being the first argument to the command, 2 as being the second argument, and so on.

You can use any event designator in conjunction with a word designator. In the following example, `!!` is the most recent command line: `avconv -i screencast.mp4 podcast.mp3`. The `!a` event designator expands to that same command since it’s the most recent command that started with the letter “a.”

```bash
$ avconv -i screencast.mp4 podcast.mp3
$ mv !!:2 converted/
mv screencast.mp4 converted/
$ mv !a:3 podcasts/
mv podcast.mp3 podcasts/
$
```

### Repeat the Previous Command While Substituting a String

```bash
$ ^<string1>^<string2>^
```

This little trick is great for quickly correcting typing mistakes. If you omit `^<string2>^`, then `<string1>` will be removed from the previous command. By
