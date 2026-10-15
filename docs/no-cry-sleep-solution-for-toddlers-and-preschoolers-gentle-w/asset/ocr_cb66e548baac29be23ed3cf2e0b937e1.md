You can suspend a job and stop it with the CTRL-Z key. This places the job to the side until it is restarted. The job is not ended; it merely remains suspended until you want to continue. When you’re ready, you can continue with the job in either the foreground or the background using the fg or bg command. The fg command restarts a suspended job in the foreground. The bg command places the suspended job in the background.

At times, you may need to place a currently running job in the foreground into the background. However, you cannot move a currently running job directly into the background. You first need to suspend it with CTRL-Z, and then place it in the background with the bg command. In the next example, the current command to list and redirect .c files is first suspended with CTRL-Z. Then that job is placed in the background.

```
$ cat *.c > myprogs
^Z
$ bg
```

# Shell Variables

The Bash, Korn, and Z shells described previously are actually types of shells. A shell, by definition, is an interpretive environment within which you execute commands. You could have many environments running at the same time, either of the same type or of different types of shells. These interpretive environments are referred to as shells. So you could have several shells running at the same time that are of the Bash shell type.

Within each shell, you could enter and execute commands. You can further enhance the capabilities of a shell using shell variables. With a shell variable, you can hold data that you could reference over and over again as you execute different commands within a given shell. For example, you could define a shell variable to hold the name of complex filename. Instead of retyping the filename in different commands, you could reference it with the shell variable.

You define variables within a shell, and such variables are known as shell variables. Many different shells exist. Some utilities, such as the Mail utility, have their own shells with their own shell variables. You can also create your own shell using what are called shell scripts. You have a user shell that becomes active as soon as you log in. This is often referred to as the login shell. Special system variables are defined within this login shell. Shell variables can also be used to define a shell’s environment, as described in Chapter 9.

> NOTE Shell variables exist as long as your shell is active—that is, until you exit the shell. For example, logging out will exit the login shell. When you log in again, any variables you may need in your login shell must be defined again.

# Definition and Evaluation of Variables: =, $, set, unset

You define a variable in a shell when you first use the variable’s name. A variable’s name may be any set of alphabetic characters, including the underscore. The name may also include a number, but the number cannot be the first character in the name. A name may not have any other type of character, such as an exclamation point, an ampersand, or even a space. Such symbols are reserved by the shell for its own use. Also, a variable name may not include more than one word. The shell uses spaces on the command line to distinguish