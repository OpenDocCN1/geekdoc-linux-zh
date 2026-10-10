The built-in variable \$ (which is, by no coincidence, also the default user prompt) is the symbol for the current shell.

To view the PID of the current shell, use the following syntax:

```
$ echo $$<Enter>
```

# Example 12.1 Checking the Shell’s PID

To view the PID of the current shell, type

```
$ echo $$<Enter>
340
```

# The Login Process

The user login process creates a Linux session that continues until the user logs out. The process environment contains all the information necessary to enable the process to run. We have seen before how Linux creates the shell environment and initiates the shell process. Generally, by default, users are placed in their own home directories and the bash shell is initiated.

# Example 12.2 Variables and Parameters for Logging in

Example 12.2 shows the typical variables and parameters required for the user login process:

+   Command: -bash  
+   UID: quixoted  
+   GID: knights1  
+   TTY: tty1  
+   PID: 340

All of the information in Example 12.2 is unique to the process environment as long as Don Quixote remains logged in. After he logs out, the information is forgotten. When he logs in again, another new process environment is created for him.