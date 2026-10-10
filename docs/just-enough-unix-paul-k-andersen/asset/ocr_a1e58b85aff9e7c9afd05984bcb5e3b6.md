# WORKING WITH THE SHELL
9.9 Interrupting a Foreground Process

# 9.9 Interrupting a Foreground Process

If you start a long-running process such as `sleep` the usual way (that is, in the foreground), you cannot work on any other commands until it finishes. If for some reason you do not wish to wait that long, you must interrupt the process. This is done with the **Ctrl**-**C** key combination.

+   1.  **Start the process.** For example,
+       ```
+       $ (sleep 120; echo I am awake now) [Return]
+       ```
+   2.  **Interrupt the process.** Type
+       ```
+       [Control] - C
+       ```
+       This will interrupt `sleep` and invoke the `echo` command:
+       ```
+       ^C I am awake now
+       $
+       ```

# 9.10 Running a Background Process

As we said before, UNIX allows you to run a process in the “background” while you work on another task in the foreground. This is useful for long-running processes, especially those that do not require your attention. As an example of such a long-running process, we will once again use the `sleep` command.

+   1.  **Start a long-running process in the background.** For example,
+       ```
+       $ (sleep 60; echo I am awake now)& [Return]
+       ```
+       If you are running the Bourne shell, you should see something like this:
+       ```
+       3271
+       ```
+       In this example, the shell assigned a process identification (PID) number of 3271. (The actual PID on your system may be different.)
+       
+       If you are running C Shell or Korn Shell, you should see something like this:
+       ```
+       [1]     3271
+       ```
+       Here, [1] is the job number and 3271 is the PID.
+       
+       The shell will display a prompt to let you know it is ready for more commands:
+       ```
+       $
+       ```
+   2.  **Check status of the process.** Enter the `ps` (“process status”) command to check on what is happening:
+       ```
+       $ ps [Return]
+       ```