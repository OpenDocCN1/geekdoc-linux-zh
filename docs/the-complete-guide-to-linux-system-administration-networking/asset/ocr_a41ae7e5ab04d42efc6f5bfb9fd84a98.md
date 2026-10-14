A shell trace lets you see if the script is really using the values you expect, and if it is executing commands in the order that you expect.

# Debugging within a Script

Although it can be very useful to start a script with the -x option, a large script generates a great deal of output that can make it hard to locate errors. For this reason, it is often more helpful to turn on debugging within a script just at the point where the script appears to be working incorrectly. You can do this using the set command with the -x option. For example, if your script includes a for loop that does not function as expected, you can enclose that loop within two set commands, enabling and then disabling the shell trace debugging function. By doing this, debugging information is only displayed for the loop causing the problem, making it easier to spot the problem:

```
set -x
for loopvar in $@
do
# process each file name that was provided on the command line
done
set +x
```

Software developers or system administrators who write many scripts often create debugging functions that they can call from different points in their scripts. Their scripts, or sometimes the debugging functions themselves, may rely on environment variables. For example, a developer might write a large script that includes several debugging features. But none of the debugging features are active by default. But when any user sets an environment variable called DEBUGME (a random variable name selected by the developer) to the value of true before executing the script, the script changes behavior, providing debugging information automatically. Resetting the DEBUGME environment variable to false causes the script to act normally, displaying no debugging information.

You can experiment with different arrangements using the set -x command and various functions within your own scripts to see what arrangement is most helpful to you. Examining scripts written by experienced administrators and developers (including those you find on a standard Linux system) is a great way to see how different tasks have already been accomplished.

# Other Programming Methods

You have learned the basics of creating shell scripts, but many other types of scripts and compiled languages are used in Linux. The statements in a shell script must follow specific syntax rules for tests, loops, and so forth. Other types of scripts are written using different computer languages and interpreted by different interpreters (rather than the bash shell). The specific syntax rules a script must follow depend on the interpreter that will execute the script.