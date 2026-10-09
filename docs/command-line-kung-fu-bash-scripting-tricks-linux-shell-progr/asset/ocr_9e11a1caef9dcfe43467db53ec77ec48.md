```
$ ls file.txt*
file.txt  file.txt.2014-04-08
$ ps -fp $(cat /var/run/ntpd.pid)
UID          PID  PPID C STIME TTY          TIME
CMD
ntp        1210     1 0 Apr06 ?
00:00:05 ntpd -u ntp:ntp -p /var/run/ntpd
$ sudo kill -9 $(cat /var/run/ntpd.pid)
$ for x in $(cut -d: -f1 /etc/passwd); do groups $x;
done
jason : jason sales
bobdjr : sales
jim : jim
```

# Store Command Line Output as a Variable to Use Later

```
$ for VAR in LIST
> do
>	VAR2=$(command)
>	VAR3=$(command)
>	echo "$VAR2 $VAR3"
> done
```

Command substitution can be used to assign values to variables. If you need to reuse the output of a command multiple times, assign it to a variable once and reuse the variable. This example shows how the output of the id command is used multiple times in one script.

```
$ for USER in $(cut -f1 -d: /etc/passwd)
> do
> UID_MIN=$(grep ^UID_MIN /etc/login.defs | awk
```