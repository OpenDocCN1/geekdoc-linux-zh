# ### 3.4.3. Managing Processes

The `ps aux` command lists the processes currently running and helps to identify them by showing their PID. Once you know the *PID* of a process, the `kill -signal pid` command allows you to send it a signal (if you own the process). Several signals exist; most commonly used are *TERM* (a request to terminate gracefully) and *KILL* (a forced kill).

The command interpreter can also run programs in the background if the command is followed by “&”. By using the ampersand, you resume control of the shell immediately even though the command is still running (hidden from view as a background process). The `jobs` command lists the processes running in the background; running `fg job-number` (for *foreground*) restores a job to the foreground. When a command is running in the foreground (either because it was started normally, or brought back to the foreground with `fg`), the *Ctrl+Z* key combination pauses the process and resumes control of the command line. The process can then be restarted in the background with `bg job-number` (for *background*).

# ### 3.4.4. Managing Rights

Linux is a multi-user system so it is necessary to provide a permissions system to control the set of authorized operations on files and directories, which includes all the system resources and devices (on a Unix system, any device is represented by a file or directory). This principle is common to all Unix-like systems.

Each file or directory has specific permissions for three categories of users:

+   - Its *owner* (symbolized by *u*, as in user)
+   - Its *owner group* (symbolized by *g*, as in group), representing all the members of the group
+   - The *others* (symbolized by *o*, as in *other*)

Three types of rights can be combined:

+   - *reading* (symbolized by *r*, as in *read*);
+   - *writing* (or *modifying*, symbolized by *w*, as in *write*);
+   - *executing* (symbolized by *x*, as in *EXecute*).

In the case of a file, these rights are easily understood: read access allows reading the content (including copying), write access allows changing it, and execute access allows running it (which will only work if it is a program).