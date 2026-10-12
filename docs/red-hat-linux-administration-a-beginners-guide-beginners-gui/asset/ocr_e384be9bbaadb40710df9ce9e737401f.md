root 468 0.0 0.2 1060 384 tty3 S Jun10 0:00 /sbin/mingetty tty3
root 469 0.0 0.2 1060 384 tty4 S Jun10 0:00 /sbin/mingetty tty4
root 470 0.0 0.2 1060 384 tty5 S Jun10 0:00 /sbin/mingetty tty5
root 471 0.0 0.2 1060 384 tty6 S Jun10 0:00 /sbin/mingetty tty6
root 473 0.0 0.0 1052 116 ? S Jun10 0:01 update (bdflush)
root 853 0.0 0.7 1708 940 pts/1 S Jun10 0:00 BASH
root 1199 0.0 0.7 1940 1012 pts/2 S Jun10 0:00 su
root 1203 0.0 0.7 1700 920 pts/2 S Jun10 0:00 BASH
root 1726 0.0 1.3 2824 1760 ? S Jun10 0:00 xterm
root 1728 0.0 0.7 1716 940 pts/8 S Jun10 0:00 BASH
root 1953 0.0 1.3 2832 1780 ? S Jun11 0:05 xterm
root 1955 0.0 0.7 1724 972 pts/10 S Jun11 0:00 BASH
nobody 6436 0.0 0.7 2572 988 ? S Jun13 0:00 httpd
nobody 6437 0.0 0.7 2560 972 ? S Jun13 0:00 httpd
nobody 6438 0.0 0.7 2560 976 ? S Jun13 0:00 httpd
nobody 6439 0.0 0.7 2560 976 ? S Jun13 0:00 httpd
nobody 6440 0.0 0.7 2560 976 ? S Jun13 0:00 httpd
nobody 6441 0.0 0.7 2560 976 ? S Jun13 0:00 httpd
root 16673 0.0 0.6 1936 840 pts/10 S Jun14 0:00 su -michael
michael 16675 0.0 0.8 1960 1112 pts/10 S Jun14 0:00 -zsh
root 18243 0.0 0.9 2144 1216 tty1 S Jun14 0:00 rwlite
rwhte 18244 0.0 0.8 1940 1080 tty1 S Jun14 0:00 -tcsh

The very first line of the output provides column headers for the listing, as follows:

+   - **Column 1: USER** Who owns what process.
+   - **Column 2: PID** Process identification number.
+   - **Column 3: %CPU** Percentage of the CPU taken up by a process. Note: For a system with multiple processors, this column will add up to more than 100 percent.
+   - **Column 4: %MEM** Percentage of memory added up by a process.
+   - **Column 5: VSZ** The amount of virtual memory a process is taking.
+   - **Column 6: RSS** The amount of actual (resident) memory a process is taking.
+   - **Column 7: TTY** The controlling terminal for a process. A question mark in this column means the process is no longer connected to a controlling terminal.
+   - **Column 8: STAT** The state of the process: