with the line the user is logged in on. The login-time is the date and time that the user logged in. The idle is the length of time since the terminal was last used (the idle time--see the --idle option. The from is the remote machine or X display that the user is logged in from (blank for local users).

# Notes

The finger utility (page 1171) provides information similar to the information who provides.

# Examples

The following examples demonstrate the use of the who utility:

```
$ who
hls tty1 Jul 30 06:01
jenny tty2 Jul 30 06:02
alex tty3 Jul 30 14:56 (bravo)
$ who am i
bravo!alex tty3 Jul 30 14:56 (bravo)
$ who --heading --idle LOGIN-TIME IDLE FROM
USER MSG LINE
hls - tty1 Jul 30 06:01 03:53
jenny + tty2 Jul 30 06:02 14:47
alex + tty3 Jul 30 14:56 (bravo)
```