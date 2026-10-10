the Bash calculator. It's important to remember that any variables created within the Bash calculator are valid only within the Bash calculator and can't be used in the shell script.

# # Exiting the Script

So far in our sample scripts, we terminated things pretty abruptly. When we were done with our last command, we just ended the script. There's a more elegant way of completing things available to us.

Every command that runs in the shell uses an *exit status* to indicate to the shell that it's done processing. The exit status is an integer value between 0 and 255 that's passed by the command to the shell when the command finishes running. You can capture this value and use it in your scripts.

# ## Checking the exit status

Linux provides the $? special variable that holds the exit status value from the last command that executed. You must view or use the $? variable immediately after the command you want to check. It changes values to the exit status of the last command executed by the shell:

```
$ date
Mon Jun 01 16:01:30 EDT 2020
$ echo $?
0
$
```

By convention, the exit status of a command that successfully completes is 0. If a command completes with an error, then a positive integer value is placed in the exit status:

```
$ asdfg
-bash: asdfg: command not found
$ echo $?
127
$
```

The invalid command returns an exit status of 127. There's not much of a standard convention to Linux error exit status codes. However, there are a few guidelines you can use, as shown in [Table 11-2](#).