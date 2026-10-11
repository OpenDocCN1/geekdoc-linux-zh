+   3. Precede the filename with `sh` so the shell will take this as an argument and execute the command (you can also try this in `ksh` or `csh`):
+      ```
+      $ sh barriers
+      ```

+   4. Use the `file` command to find out what kind of shell script you're accessing. If the type of script is unknown, the `file` command will report that it’s an ASCII file, which is usually what a Bourne shell script is.

# ## Job Control

Job control enables you to move jobs to the background, bring them to the foreground, or stop them. This function gives the user greater flexibility and efficiency while working. Jobs may be running behind the scenes while the desktop is active. A command pipeline or multiple commands on a single command line are good examples of jobs.

The names of individual jobs are followed by the `&`. If the `&` is trailing the command, it signals to the shell to run the job in the background. The shell will display information about background jobs. It will provide a job number in brackets and the process identification (PID) number of the final process in the job. There is a specific shell aptly named the Job shell (`jsh`); the Bourne shell does not support job control. In addition to having all the capabilities and built-ins of the Bourne shell, the Job shell fully supports job control. The Korn shell and C shell both support job control as well.

Solaris also has a utility named `jobs` in the Bourne shell. It lists all background jobs. Even though Bourne does not support job control, it will not generate an error message if you give the `jobs` command. It will allow you to enter the `sleep` command, which will create a background job that the utility can report on. The `jsh` command will then invoke the Job shell while the `jobs` utility displays job information.

Before issuing a prompt, the Job shell will issue a list of job numbers and PID numbers of any jobs running in the background. One or more of these jobs may be moved into the foreground by using the `fg` built-in with a `%` sign preceding the job number. If there is only one job running in the background or it is listed with a `+` sign, you can use `fg` without arguments.

Conversely, if you want to send a foreground job to the background, you must press `Ctrl+z` or `Ctrl+y`. This will suspend the job immediately (`Ctrl+z`) or after it tries to read input from the terminal (`Ctrl+y`). You need to use the `bg` built-in because `Ctrl+y` or `Ctrl+z` puts the commands into a suspended mode and you have to tell them to reactivate in the background. When a background job reads from the terminal, the shell will put it to sleep until you give further input. Move the job into the foreground so it can read from the terminal. The command line will be displayed. The shell will let you know about the status of a job. It will tell you step-by-step when the job begins, ends, or is waiting for further input. The shell will delay disrupting your