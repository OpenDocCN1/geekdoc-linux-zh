```
var1=10.46
var2=43.67
var3=33.2
var4=71
```

```
var5=bc << EOF
scale = 4
a1 = ($var1 * $var2)
b1 = ($var3 * $var4)
a1 + b1
EOF
```

echo The final answer for this mess is $var5\$

Using this you can place each option and expression on a separate line in your script, making things cleaner and easier to read and follow. The EOF string indicates the start and end of the data to redirect to the bc command. Of course, you need to use the backtick characters to indicate the command to assign to the variable.

You'll also notice in this example that you can assign variables within the bash calculator. It's important to remember that any variables created within the bash calculator are only valid within the bash calculator and cannot be used in the shell script.

# Exiting the Script

So far, in our sample scripts we terminated things pretty abruptly. When we were done with our last command, we just ended the script. There's a more elegant way of completing things available to us.

Every command that runs in the shell performs an exit status to indicate to the shell that it's done processing. The exit status is an integer between 0 and 255 that is passed by the command to the shell when the command finishes running. You can capture this value and it in your scripts.

# Checking the exit status

Linux provides the ?$ special variable that holds the exit status value from the last command executed. You must view or use the $? variable immediately after the command you want to check. It changes values to the exit status of the last command executed by the shell:

+   $ date
Sat Sep 29 10:01:30 EDT 2007
$ echo $?
0
$