# Examples

The first example shows a command line executing the first kill compute as a-ground process and the kill utility terminating it:

```
$ compute &\n[2] 259
$ kill 259
$
[2] + terminated compute
```

The next example shows the ps utility determining PID number of the-ground process running a program named xprog and the kill utility terminating xprog with the TERM signal:

```
$ ps
PID TTY STAT TIME COMMAND
116 1 S 0:00 -zsh
128 1 S N 0:00 xinit /home/alex/.xinitrc --
137 1 S N 0:01 fvwm
138 p0 S N 0:00 -zsh
161 p0 S N 0:10 xprog
262 p0 R N 0:00 ps
$ kill -TERM 161
[1] + killed xprog
$ 
```