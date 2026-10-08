# 246 LOCALIZATION

To ensure that XTerm interprets the Home and End keys as you expect, you must insert the lines shown in Listing 9.4 in ~/.Xresources.

Listing 9.4 Keyboard assignment in xterm.

If after, these programs as joe or emacs do not react to these keys in XTerm, the file /etc/termcap must be adapted as well. For the xterm device, the following entries should be available in termcap:

```
:kh\=E[1~:ki=E[2~:kD=E[3~:kh=\=E[4~
```

To define your own keyboard assignments under X, you can use a program such as xcaps, for example, which allows you to create and test an input filter for xmodmap under X in a menu-driven interactive way.

The program was contributed to the X Consortium to be distributed as a free extra with the X Window system. Therefore, it can be found on the ftp server ftp.x.org and all systems that mirror this server.

| Additional Information and Sources |
|---||
| Man pages: | xcaps(ix), |
| Package: | xcaps-2.25.tar.gz |
| ftp server: ftp.x.org |
| ftp path: /R5contrib |
| Size: about 140 Kbytes |

# 9.4 Use of foreign language characters at the shell level

After logging in to the LINUX system, a shell is started which accepts user input and launches programs. As a rule, no special characters such as umlauts or accented letters should be used in file names in many (older) UNIX systems, this can lead to problems because such files can be very hard to delete.