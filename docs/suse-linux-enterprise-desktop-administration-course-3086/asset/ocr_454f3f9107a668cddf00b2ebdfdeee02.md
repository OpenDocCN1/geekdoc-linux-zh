![](bbox=[0.025, 0.066, 0.212, 0.138])

# Exercise 10-3: Manage Linux Processes

In this exercise, start and stop processes and change their priorities. First, start and suspend `xeyes`, move it to the background and foreground, and stop it. Then, start `xeyes` and set the priority of the running program to a nice value of -5. Start a second `xeyes` with a nice value of 10.

# Detailed Steps to Complete This Exercise

Part I: Manage Processes

Part II: Modify Process Priorities

# Part I: Manage Processes

To move processes to the background, do the following:

+   1. Make sure you are logged in to the GNOME desktop as geeko.
+   
+   2. Open a terminal window and display the processes that are currently owned by geeko by entering
+   
+      ```bash
+      ps -lU geeko (lowercase L)
+      ```
+   
+   3. Display the processes that are currently owned by root by entering
+   
+      ```bash
+      ps -lU root (lowercase L)
+      ```
+   
+   4. Start the program `xeyes` by entering
+   
+      ```bash
+      xeyes
+      ```
+   
+      Notice that the terminal is not available to receive new commands (no command-line is displayed) because the `xeyes` program is running in the foreground.
+   
+   5. Arrange the `xeyes` window and the terminal window so that you can see them both; then select the terminal window to activate it.
+   
+   6. Suspend the `xeyes` program by pressing
+   
+      ```text
+      Ctrl+z
+      ```
+   
+      Notice that the eyes are no longer following the cursor.
+   
+   7. View the job in the background by entering
+   
+      ```bash
+      jobs
+      ```
+   
+   8. View the `xeyes` process running from the current terminal by entering
+   
+      ```bash
+      ps -l (lowercase L)
+      ```
+   
+      The process shows a status of T, which means that it is being traced or stopped.
+   
+   9. Resume the `xeyes` program running in the background by entering
+   
+      ```bash
+      bg 1 (the number one)
+      ```
+   
+      The `xeyes` program is running again (notice the eyes following the cursor again).