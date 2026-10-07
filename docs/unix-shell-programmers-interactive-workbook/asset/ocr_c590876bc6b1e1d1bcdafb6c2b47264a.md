# 526 Lab 11.2: The exec Command

Using the KornShell to build a web browser may seem to be an odd thing to do, but it is actually an example of what shell programming is very good for:We were able to write a few lines of code to check out our connection to the server.Writing the equivalent “quick and dirty” program in C could have taken dozens of lines of code.

![](bbox=[0.135, 0.103, 0.213, 0.168])

LAB 11.2

# LAB 11.2 SELF-REVIEW QUESTIONS

To test your progress, you should be able to answer the following questions:

+   1) What would a script named doit containing the following commands if you do it from an interactive shell prompt?

```
[[ -n $DO1 ]] && exec do1
[[ -n $DO2 ]] && exec do2
print did not do do1 and did not do2.
```

+   a) If DO1 is a non-zero-length string, execute command do1, then if DO2 is a non-zero-length string, execute command do2, then print the message.
b) If DO1 is a non-zero-length string, execute the command do1 and log off the system. But if DO1 is not a non-zero-length string, and DO2 is a non-zero-length string, execute the command do2, and log off the system. Neither DO1 nor DO2 is a non-zero-length string, print the message and prompt for the next command line.
c) If DO1 is a non-zero-length string, execute the command do1 and log off the system. But if DO1 is not a non-zero-length string, and DO2 is a non-zero-length string, execute the command do2, and log off the system. Neither DO1 nor DO2 is a non-zero-length string, print the message, and log off the system.
d) It always prints “Do what you done done done!"
e) It logs you off the system and sends e-mail to the administrator reporting your attempt to perform an illegal operation.

+   2) A script contains the following lines of code.What is going on here?

```
exec 0 < commands
a_prog
exec 0 < /dev/tty
```