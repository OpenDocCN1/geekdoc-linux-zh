Other programs evaluate the environment variable LANG, which can be used to set the country's language (in the following example, the German language):
# Addition to /etc/profile or ~/.bashrc
export LANG=de_DE.ISO-8859-1

Many other programs possess their own environment variables or configuration files, which have to be adjusted. Special information on the Less program (text display) and the Emacs editor can be found on pages 139 and 539.

A remark regarding profile: this is automatically executed by the shell at each login. It is therefore particularly suitable for the definition of system variables and abbreviations. Background information on profile can be found on page 425.

Unfortunately, Linux does not yet know the Euro symbol. (To be precise, this is not a problem of the Linux kernel, but the programs running under Linux and of the individual distributions. The kernel supports Unicode.) Until a standard has emerged, you will need to use special character sets and change the keyboard table manually (and this, functions only for a very limited number of programs). A package including the required character sets and further information is available on the Internet:

```
ftp://ftp.freshmeat.net/pub/euro-patch/
```

# Time of day

Under DOS, the system time is simply taken from your computer CMOS clock. Linux, things are not that easy. Because of their virtually international network, Unix computers worldwide use one and the same time. GMT stands for Greenwich Mean Time, which is the measure of all things (at least timewise) on Unix computers.

When you store a file, the stored time is not the current local time, but a time that is converted to this international standard. When, later on, you look at the file with -l, that time is reverted to the local time at the location of the computer. This complicated-looking procedure allows you to determine which file is 'more recent': a file stored in Munich at 18:00 local time, or a file stored in New York at 12:30 local time.

To make all this work, Linux must first know in time zone the computer is located. Depending on the distribution, setting the time zone is carried out via different files:

+   Debian: /etc/timezone
RedHat: /etc/localtime
SuSE: /etc/rc.config

To be accurate, /etc/localtime is not a normal file, but a link to the time zone file. The following command shows how this link is created (for RedHat).