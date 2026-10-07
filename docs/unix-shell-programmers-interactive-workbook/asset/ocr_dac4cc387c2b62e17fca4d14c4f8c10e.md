# LAB 11.3 EXERCISES

```
11.3.1 INTERCEPT INT AND EXIT TRAPS
```

If you ever pressed Ctrl-C to stop a program, you've delivered a signal to a process. It's not as convenient, but you could accomplish the same thing using the system's kill command.

If you have changed your interrupt character to something other than Ctrl-C, either mentally change all references to "Ctrl-C" in this exercise to whatever character you are using, or run the following command before proceeding:

```
stty intr ^C
```

That's literally the characters caret (^) and () at the end of the line, not Ctrl-C.

For this exercise, we will use the following program to study trap processing. Put it in a script named tti for "first trap test":

```
# trap-test 1
nsleep 30
print -- "$0 Completed Normally"
```

If you run the program in the foreground and press Ctrl-C while it is running, it will terminate, and nothing will print. Not very interesting. However, run it in the background by ending the command line with an ampersand (&), as discussed in Exercise 3.1.2,"Parallel execution (&)," and observe the job and process numbers that are displayed. Assuming that job number is [1], enter the following command during the 30 seconds that tti is sleeping:

```
kill -INT %1
```

Alternatively, you could use the process number in place of the %1 at the end of that command.