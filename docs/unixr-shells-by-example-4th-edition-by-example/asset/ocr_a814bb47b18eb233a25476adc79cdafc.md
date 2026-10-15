# EXAMPLE 14.68 (CONTINUED)

```
In the main script
In trapper
Still in main
The pid is 4267
Caught in a trap!      # User just pressed Ctrl-C
In the main script
```

# EXPLANATION

+   1. The trapper function is defined. All variables and traps set in the function are global to the script.
+   2. The trap command will ignore INT, signal 2, the interrupt key (^C). If ^C is pressed, the message Caught in a trap! is printed, and the script continues forever. The script can be killed with the kill command or Ctrl\.
+   3. The main script starts a forever loop.
+   4. The function trapper is called.
+   5. When the function returns, execution starts here.
+   6. The PID will be displayed. Later you can use this number to kill the process from another terminal. For example, if the PID is 4267, the kill 4267 will terminate this process.
+   7. The program pauses (sleeps) for 5 seconds.

# 14.9 Debugging

By using the -n option to the bash command, you can check the syntax of your scripts without really executing any of the commands. If there is a syntax error in the script, the shell will report the error. If there are no errors, nothing is displayed.

The most commonly used method for debugging scripts is the set command with the -x option, or bash invoked with the -x option and the script name. See Table 14.7 for a list of debugging options. These options allow an execution trace of your script. Each command from your script is displayed after substitution has been performed, and then the command is executed. When a line from your script is displayed, it is preceded with a plus (+) sign.

With the verbose option turned on, or by invoking the shell with the -v option (bash -v scriptname), each line of the script will be displayed just as it was typed in the script, and then executed. (See Chapter 15, "Debugging Shell Scripts," on page 967 for details.)