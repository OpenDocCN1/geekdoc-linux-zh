# # Kill

20

kill doesn't just kill programs

Which signal kill sends

# kill -l lists all signals

![](bbox=[0.035, 0.275, 0.315, 0.435])

| name | num |
|---|---|
| kill | SIGTERM 15 |
| kill -9 | SIGKILL 9 |
| kill -KILL | | |
| kill -HUP | SIGHUP 1 |
| kill -STOP | SIGSTOP 19 |

+   1 HUP 2 INT 3 QUIT 4 ILL
5 TRAP 6 ABRT 7 BUS 8 FPE
9 KILL 10 USR 11 SEGV 12 USR
13 PIPE 14 ALRM 15 TERM 16 SIGFLT
17 CHILD 18 CONT 19 STOP 20 TTSP
21 TINT 22 TTO 23 URG 24 XCPU
25 XFS 26 VTLARM 27 PROF 28 WINCH
29 POLL 30 PWR 31 SYS

kill -SIGNAL PID name or number

# # pgrep

# # pkill

# killall -SIGNAL NAME

signals all processes called NAME for example
$ killall firefox

prints PIDs of matching running programs

same as pgrep, but signals PIDs found. ex:

useful flags:

pgrep matches firefox firebird
NOT bash firefox.sh

pkill -f firefox

+   -w wait for all signaled processes to die

To search the whole command line (eg bash firefox.sh)
use pgrep -f

+   -i ask before signalling

![](bbox=[0.685, 0.835, 0.965, 0.945])