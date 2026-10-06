# Chapter 17 Red Linux System Administration

for a user. To kill a process, you need to know the PID of the process. The ps utility can give you this information if you know the name of the program the user is running/or the name of the user.

In this example Alex claims that Netscape (www.netscape.com) is stuck and he cannot do anything from the Netscape window, not even close. A more experienced user could open another window and kill the process, but in this case it will be for Alex. First, use ps with the -u option, followed by the name of the user and the -f (full/wide) option to view all processes associated with that user:

$ ps -u alex -f

| UID PID CTIME CMD |
|---|---|---|---|-|
| alex | 2841 | 2840 | 09:39 tty1 | 00:00:00 -bash |
| alex | 2896 | 2841 | 09:40 tty1 | 00:00:00 /bin/sh /usr/X11R6/bin/start |
| alex | 2903 | 2896 | 09:40 tty1 | 00:00:00 xinit /etc/X11/xinitrcxrc |
| alex | 2908 | 2903 | 09:40 tty1 | 00:00:00 /bin/bash /usr/bin/startkde |
| alex | 2974 | | 01:41 ? | 00:00:00 kdeit:dclopserver --nosid |
| alex | 2977 | | 01:41 ? | 00:00:00 kdeit:klauncer |
| alex | 2980 | | 01:41 ? | 00:00:00 kdeit:kdeded |
| alex | 3002 | | 01:41 ? | 00:00:00 /bin/bin/arts -F 10 -S 4096 -s 60 |
| alex | 3008 | | 01:41 ? | 00:00:00 kdeit:notify |
| alex | 3009 | | 01:41 ? | 00:00:00 kdeit:Running... |
| alex | 3010 | 3010 | 09:41 tty1 | 00:00:00 kmserver -restore |
| alex | 3012 | 3009 | 01:41 ? | 00:00:00 kdeit:kwin |
| alex | 3014 | | 01:41 ? | 00:00:00 kdeit:kdestop |
| alex | 3019 | | 01:41 ? | 00:00:01 kicker |
| alex | 3024 | | 01:41 ? | 00:00:00 kdeit:klipper -icon klipper |
| alex | 3028 | | 01:41 ? | 00:00:00 kdeit:kwrited |
| alex | 3029 | | 01:41 ? | 00:00:00 alarm |
| alex | 3030 | 3028 | 01:41 pts/2 | 00:00:00 /bin/cat |
| alex | 3040 | 3009 | 01:41 ? | 00:00:00 konsole -icon console |
| alex | 3041 | 3040 | 01:41 pts/3 | 00:00:00 /bin/bash |
| alex | 3069 | | 01:41 ? | 00:00:00 kdeit:control -caption Control |
| alex | 3074 | 3041 | 01:42 pts/3 | 00:00:03 /usr/lib/netscape/netscape-communi |
| alex | 3101 | 3074 | 01:42 pts/3 | 00:00:00 (ns helper) |
| alex | 3213 | 3114 | 01:49 ? | 00:00:41 kcience.kk -window-id 4194310 |

This list is fairly short and easy to find. Use ps to produce a long list of all the processes and then use grep to find the processes running Netscape:

$ ps -ef | grep netscape

| alex 3074 1 10:22 tty1 00:00:01 /usr/lib/netscape/netscape-commu- |
| alex 3157 2573 0 10:25 pts/1 00:00:00 grep netscape |

Many people may be running Netscape, and you may need to look in the left column to find the name of the user so you can kill the process. You can combine the two commands as -ps -u alex -f | grep process.

Now that you know the PID (3074) of Alex running Netscape, you can use kill to terminate it. The safest way to do this is in Alex as Alex (allows