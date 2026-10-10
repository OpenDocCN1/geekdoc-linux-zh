+   20. Which command can be used to see processes running in the background?
+   a. bg
+   b. jobs
+   c. ps -%
+   d. fg

# Hands-on Projects

![](bbox=[0.08, 0.27, 0.25, 0.35])

These projects should be completed in the order given. The hands-on projects presented in this chapter should take a total of three hours to complete. The requirements for this lab include:

+   * A computer with Fedora Linux installed according to Hands-on Project 2-1

# Project 9-1

In this hands-on project, you view characteristics of processes using the `ps` command.

+   1. Boot your Fedora Linux virtual machine. After your Linux system has been loaded, switch to a command-line terminal (tty2) by pressing Ctrl+Alt+F2 and log in to the terminal using the user name of root and the password of LNXRocks!.
+   
+   2. At the command prompt, type `ps -ef | less` and press `Enter` to view the first processes started on the entire Linux system.
+   
+   3. Fill in the following information from the data displayed on the terminal screen after typing the command:
+      a. Which process has a Process ID of 1? (PID = 1) ______________________
+      b. What character do most processes have in the terminal column (tty)? __________
+      c. What does this character in the terminal column indicate? ______________________
+      d. Which user started most of these processes? ______________________
+      e. Most processes that are displayed on the screen are started by a certain parent process indicated in the Parent Process ID column (PPID). Which process is the parent to most processes? __________
+   
+      Type `q` at the MORE prompt to quit.
+   
+   4. At the command prompt, type `ps -el | less` and press `Enter` to view the process states for the first processes started on the entire Linux system.
+   
+   5. Fill in the following information from the data displayed on the terminal screen after typing the command:
+      a. What character exists in the State (S) column for most processes, and what does this character indicate? __________
+      b. What range of numbers is it possible to have in the Nice (NI) column? __________