![](bbox=[0.17, 0.17, 0.25, 0.27])

> As a regular user, you can renice your own processes, but only within the range of 0-19. It is not possible for you to make your jobs more important than the standard nice level of zero.

4. The renice command has some additional options, not the least of which is that you can change the priority of all processes owned by a specific user in a single fell swoop. For example, if user taylor has been whining just a bit too much about slow computers and how Quake just doesn't zip along like his machine at home, you might like to slow things down even further by lowering his priority for a short period of time:

```
# renice +1 -u taylor
582: old priority 0, new priority 1
537: old priority 0, new priority 1
```

More likely, you'll want to perhaps improve the throughput of your Web server by setting all the Apache processes to have a slightly higher priority. First, let's use the -U flag to ps to limit output to just the specified UID, then renice all the relevant jobs:

```
# ps -IU apache
F S UID PID PPID C PRI NI ADDR SZ WCHAN TTY TIME CMD
140 S 48 13366 629 0 69 0 - 11689 semop ? 00:00:00 httpd
140 S 48 13367 629 0 69 0 - 11696 semop ? 00:00:00 httpd
140 S 48 13368 629 0 69 0 - 11686 semop ? 00:00:00 httpd
140 S 48 13369 629 0 69 0 - 11695 semop ? 00:00:00 httpd
140 S 48 13370 629 0 69 0 - 11689 semop ? 00:00:00 httpd
140 S 48 14993 629 0 69 0 - 11689 do_sel ? 00:00:00 httpd
140 S 48 14118 629 0 69 0 - 11693 semop ? 00:00:00 httpd
140 S 48 14322 629 0 69 0 - 11686 semop ? 00:00:00 httpd
# renice -1 -u apache
48: old priority 0, new priority -1
```

In this case, it reports the real group ID of all the processes running that match. To see that this is the case, use the -G flag (show group IDs) to ps with the number given (48):

```
# ps -IG 48
F S UID PID PPID C PRI NI ADDR SZ WCHAN TTY TIME CMD
140 S 48 13366 629 0 69 -1 - 11689 semop ? 00:00:00 httpd
140 S 48 13367 629 0 69 -1 - 11696 semop ? 00:00:00 httpd
140 S 48 13368 629 0 69 -1 - 11686 semop ? 00:00:00 httpd
140 S 48 13369 629 0 69 -1 - 11695 semop ? 00:00:00 httpd
140 S 48 13370 629 0 69 -1 - 11689 semop ? 00:00:00 httpd
140 S 48 14993 629 0 69 -1 - 11689 do_sel ? 00:00:00 httpd
140 S 48 14118 629 0 69 -1 - 11693 semop ? 00:00:00 httpd
140 S 48 14322 629 0 69 -1 - 11686 semop ? 00:00:00 httpd
```