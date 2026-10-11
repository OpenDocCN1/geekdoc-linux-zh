Normally, each process will respond as it is supposed to when it receives a SIGHUP. However, a process can also be told to ignore SIGHUP signals, which will allow it to remain running even if you log out of your shell session. This is done by using the nohup utility to run the program. This causes the process created by the command to ignore all SIGHUP signals.

For example, suppose you’ve created a shell script called updatedatymdb that automatically updates a database with information from an external data source. This script takes a long time to run (usually overnight), and you don’t want to leave your system logged in while it runs. You could enter nohup updatedatymdb & at the shell prompt and then log out. If the command generates output that is usually sent to the stdout, nohup will redirect the output to the ~/nohup.out file.

It’s important to note that a command run under nohup is only immune to SIGH-UP signals. All other kill signals still work. For example, you could terminate the program while it’s running using the SIGTERM signal with kill.

Let’s practice working with Linux processes in the following exercise.

# Exercise 13-1: Working with Linux Processes

![](bbox=[0.115, 0.485, 0.23, 0.535])

For more information watch *Exercise 13-1*.

In this exercise, you will practice using shell commands to manage processes running on your system. Complete the following:

+   1. Boot your Linux system and log in as a standard user.
+   2. Open a terminal session.
+   3. Switch to your root user account by entering `su -` followed by your root user's password.
+   4. Practice starting system processes by doing the following:
+      a. At the shell prompt, enter `rcstat status`. What's the status of `atd` daemon? (For most distributions, the `atd` daemon is not configured to run by default.)
+      b. Start the `atd` daemon by entering `rcstat start` at the shell prompt.
+      c. Enter `rcstat status` again at the shell prompt. The `atd` service should now be shown as running.
+   5. Practice using `top` by doing the following:
+      a. At the shell prompt, enter `top`.
+      b. View your running processes.
+      c. Press `H` to access the `top` help screen. Which keystroke will sort the display by CPU stats?
+      d. Press `T` to sort the display by CPU stats. Which processes are using the most CPU time on your system?
+      e. Press `M` to sort the display by memory usage. Which processes are using the most memory?