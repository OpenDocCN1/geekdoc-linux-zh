# EXAMPLE 11.68

```
(The Command Line)
1 $ cat << DONE
>Hello there
>what's up?
>Bye now The time is $(date).

2 > DONE

3 Hello there
What's up?
Bye now The time is Sun May 30 19:48:23 PDT 2004.
```

# EXPLANATION

+   1 The cat program accepts input until DONE appears on a line by itself. The << operator allows the final terminator to be preceded by one or more tabs. (The > is the shell's secondary prompt.)
+   2 The final matching DONE terminator is preceded by a tab. From the first DONE on line 1 to the last DONE on this line, the text in between is sent as input to the cat command.
+   3 The output of the cat program is displayed on the screen.

# 11.15 Timing Commands

# 11.15.1 The time Command

The time command is a ksh built-in command. The time command prints the following to standard error: elapsed time, the user time, and the system time used to execute a command.

# EXAMPLE 11.69

```
1 $ time sleep 3
real 0m3.15s took 3.15 seconds to run
user 0m0.01s sleep used its own code for .01 seconds
sys 0m0.08s and kernel code for .08 seconds

2 $ time ps -ef | wc -l # time is measured for all commands in the pipeline
38
real 0m1.03s
user 0m0.01s
sys 0m0.10s
```