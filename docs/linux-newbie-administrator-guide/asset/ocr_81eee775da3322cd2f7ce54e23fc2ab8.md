4.2.10 Can I set 32-bit hard drive IO? [p 71]

# 4.3 Working with X-windows

+   4.3.1 How do I install kde on RedHat 5.2? [p 72]
4.3.2 How do I set up my video card, monitor and mouse for the X-server? [p 74]
4.3.3 How to X-window remotely? [p 74]
4.3.4 Can I have multiple sessions of X running at the same time? [p 76]
4.3.5 Can I have a GUI login prompt? [p 76]

# 4.5 Printer and soundcard

+   4.4.1 How to set up my soundcard? [p 77]
4.4.2 How do set up my printer? [p 78]
4.4.3 Word Perfect 8 does not have a driver for my printer [p 80]

# 4.6 Setting up a network

+   4.5.1 Would it be worth it to set up my home network? [p 80]
4.5.2 How to set up my home network? [p 80]
4.5.3 I have problems configuring the ppp dial out [p 83]
4.5.4 How to browse the net from my networked computer without a modem? [p 85]
4.5.5 How do I use Samba? [p 86]
4.5.6 Sendmail [p 88]
4.5.7 Simple web server (running Apache) [p 89]
4.5.8 Simple ftp server [p 90]
4.5.9 How can one access my computer from the outside world when I am on the net using my ppp connection? [p 91]
4.5.10 Can my home computer get hacked? [p 92]

# Linux Newbie Administrator FAQ

# 4.1 LILO issues

# 4.1.1 Linux cannot detect all my memory

If you have more than 64 megabytes of physical memory, Linux kernel ver. 2.0.36 or lower will use, by default, only the first 64 MB. To see how much memory Linux uses on your system, type:

```
cat /proc/meminfo
```

You can check your version of Linux kernel with:

```
uname -a
```