+   c. Which processes have the number 4 in the Flag (F) column, and what does this number indicate? ____________________  
+   Type **q** at the MORE prompt to quit.

+   6. At the command prompt, type `ps -ef | grep z` and press **Enter** to display zombie processes on your Linux system. Are there any zombie processes indicated in the State (S) column?

+   7. Type `exit` and press **Enter** to log out of your shell.

# Project 9-2

In this hands-on project, you use kill signals to terminate processes on your system.

+   1. On your Fedora Linux virtual machine, switch to a command-line terminal (tty2) by pressing **Ctrl+Alt+F2** and log in to the terminal using the user name of **root** and the password of **LNXr0cks!**.

+   2. At the command prompt, type `ps -ef | grep bash` and press **Enter** to view the bash shells that are running in memory on your computer. Record the PID of the bash shell running in your terminal (tty2): ____________________.

+   3. At the command prompt, type `kill -1` and press **Enter** to list the available kill signals that you can send to a process.

+   4. At the command prompt, type `kill -2 PID` (where **PID** is the PID that you recorded in Question 2) and press **Enter**. Did your shell terminate?

+   5. At the command prompt, type `kill -3 PID` (where **PID** is the PID that you recorded in Question 2) and press **Enter**. Did your shell terminate?

+   6. At the command prompt, type `kill -15 PID` (where **PID** is the PID that you recorded in Question 2) and press **Enter**. Did your shell terminate?

+   7. At the command prompt, type `kill -9 PID` (where **PID** is the PID that you recorded in Question 2) and press **Enter**. Did your shell terminate? Why did this command work when the others did not?

# Project 9-3

In this hands-on project, you run processes in the background, kill them using the `kill` and `killall` commands, and change their priorities using the `nice` and `renice` commands.

+   1. On your Fedora Linux virtual machine, switch to a command-line terminal (tty2) by pressing **Ctrl+Alt+F2** and log in to the terminal using the user name of **root** and the password of **LNXr0cks!**.

+   2. At the command prompt, type `sleep 6000` and press **Enter** to start the `sleep` command, which waits 6000 seconds in the foreground. Do you get your prompt back after you enter this command? Why? Send the process an INT signal by typing the **Ctrl+c** key combination.

+   3. At the command prompt, type `sleep 6000&` and press **Enter** to start the `sleep` command, which waits 6000 seconds in the background. Observe the background Job ID and PID that is returned.