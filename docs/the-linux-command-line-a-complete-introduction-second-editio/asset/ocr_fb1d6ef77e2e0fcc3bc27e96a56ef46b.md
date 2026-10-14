```
ioctl
sfdisk (8)      - partition table manipulator for Linux
sgdisk (8)      - Command-line GUID partition table (GPT)
manipulator fo..
```

The first field in each line of output is the name of the man page, and the second field shows the section. Note that the man command with the -k option performs the same function as apropos.

# whatis—Display One-line Manual Page Descriptions

The whatis program displays the name and a one-line description of a man page matching a specified keyword.

```
[me@linuxbox ~]$ whatis ls
ls              (1)  - list directory contents
```

# THE MOST BRUTAL MAN PAGE OF THEM ALL

As we have seen, the manual pages supplied with Linux and other Unix-like systems are intended as reference documentation and not as tutorials. Many man pages are hard to read, but I think the grand prize for difficulty has got to go to the man page for bash. As I was doing research for this book, I gave the bash man page careful review to ensure that I was covering most of its topics. When printed, it’s more than 80 pages long and extremely dense, and its structure makes absolutely no sense to a new user.

On the other hand, it is very accurate and concise, as well as being extremely complete. So check it out if you dare and look forward to the day when you can read it and it all makes sense.

# info—Display a Program's Info Entry

The GNU Project provides an alternative to man pages for their programs, called info. Info manuals are displayed with a reader program