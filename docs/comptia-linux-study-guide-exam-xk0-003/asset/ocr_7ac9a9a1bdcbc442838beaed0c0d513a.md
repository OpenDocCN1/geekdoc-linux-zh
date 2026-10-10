# Listing 3.1: Output of ps -u rodsmith --forest

```
$ ps -u rodsmith --forest
  PID TTY      TIME CMD
2451 pts/3    00:00:00 bash
2551 pts/3    00:00:00 ps
2496 7        00:00:00 kvt
2498 pts/1    00:00:00 bash
2505 pts/1    00:00:00  \_ ned1t
2506 ?        00:00:00     \_ csh
2544 ?        00:00:00       \_ eye
19221 ?      00:00:01 dfm
```

# Listing 3.2: Output of ps u U rodsmith

```
$ ps u U rodsmith
USER     PID %CPU %MEM   VSZ   RSS TTY      STAT START   TIME COMMAND
rodsmith 19221  0.0   1.5  4484  1984 ?  S May07  0:01 dfm
rodsmith 2451  0.0   0.8  1856 1048 pts/3 S 16:13  0:00 -bash
rodsmith 2496  0.2   3.2  6232 4124 ? S 16:17  0:00 /opt/kd
rodsmith 2498  0.0   0.8  1860 1044 pts/1 S 16:17  0:00 bash
rodsmith 2505  0.1   2.6  4784 3332 pts/1 S 16:17  0:00 ned1t
rodsmith 2506  0.0   0.7  2124 1012 ? S 16:17  0:00 /bin/c
rodsmith 2544  0.0   1.0  2576 1360 ? S 16:17  0:00 ey
rodsmith 2556  0.0   0.7  2588  916 pts/3 R 16:18  0:00 ps u U
```

The output produced by ps normally begins with a heading line, which displays the meaning of each column. Important information that might be displayed (and labeled) includes the following:

**Username**   The name of the user who runs the programs. Listings 3.1 and 3.2 restricted this output to one user to limit the size of the listings.

**Process ID**   The process ID (PID) is a number that's associated with the process. This item is particularly important because you need it to modify or kill the process, as described later in this chapter.

**Parent process ID**   The parent process ID (PPID) identifies the process's parent. (Neither Listing 3.1 nor Listing 3.2 shows the PPID, though.)

**TTY**   The teletype (TTY) is a code used to identify a terminal. As illustrated by Listings 3.1 and 3.2, not all processes have TTY numbers-X programs and daemons, for instance, do not. Text-mode programs do have these numbers, though, which point to a console, xterm, or remote login session.

**CPU time**   The TIME and %CPU headings are two measures of CPU time used. The first indicates the total amount of CPU time consumed, and the second represents the percentage