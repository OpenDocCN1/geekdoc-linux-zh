# Linux Hack

Ajay Kumar Tiwari

[Note: 6th column with value -10 is the nice value of the shell-script.]

# Hack 101. Renice Command

Renice alters the scheduling priority of a running process.

How to decrease the priority of a running process? (Increase nice)

In the example below, an existing shell-script is running at nice value of 10.

(6th column in the ps output)

```
$ ps axl | grep nice-test
0509 13245 13216 30 10 5244 968 wait
pts/10:00 /bin/bash ./nice-test.sh
SN
```

To increase the nice value (thus reducing the priority), execute the renice command as shown below.

```
$ renice 16 -p 13245
13245: old priority 10, new priority 16
$ ps axl | grep nice-test
0509 13245 13216 36 16 5244 968 wait
pts/10:00 /bin/bash ./nice-test.sh
SN
```

[Note: Now, the 6th column of the nice-test.sh (PID 13245) shows the new nice value of 16.]

How to increase the priority of a running process? (Decrease nice)

In the example below, an existing shell-script is running at a nice value of 10.

134