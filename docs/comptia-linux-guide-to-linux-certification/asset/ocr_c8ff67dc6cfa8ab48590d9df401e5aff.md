+   4. While in the top utility, press the h key and observe the output. When finished, press the h key to return to the previous top output.
+   5. By observing the output under the COMMAND column on your terminal screen, identify the PID of the top command in the output and record it here: _______
+   6. Type r in the top utility to change the priority of a running process. When asked which process to change (renice), type the PID from the previous question. When asked which value to use, type 10 to lower the priority of the top process to 10. Does this new priority take effect immediately?
+   7. Type k in the top utility to send a kill signal to a process. When asked which process, type the PID used in the previous question. When asked which signal to send, type 2 to send an INT signal. Did the top utility terminate?
+   8. At the command prompt, type top and press Enter.
+   9. By observing the output under the COMMAND column on your terminal screen, identify the PID of the top command in the output and record it here: _______
+   10. Type k in the top utility to send a kill signal to a process. When asked which process, type the PID from the previous question. When asked which signal to send, type 15 to send a TERM signal. Did the TERM signal allow top to exit cleanly?
+   11. At the command prompt, type clear and press Enter to clear the screen.
+   12. Type exit and press Enter to log out of your shell.

# Project 9-5

In this hands-on project, you schedule processes by using the at and crontab utilities.

+   1. On your Fedora Linux virtual machine, switch to a command-line terminal (tty2) by pressing Ctrl+Alt+F2 and log in to the terminal using the user name of root and the password of LnxRocks!.
+   2. Schedule processes to run 1 minute in the future by typing the command at now + 1 minute at a command prompt, then press Enter.
+   3. When the at> prompt appears, type the word date > /root/datefile and press Enter.
+   4. When the second at> prompt appears, type the word who >> /root/datefile and press Enter.
+   5. When the third at> prompt appears, press the Ctrl+d key combination to finish the scheduling and observe the output. When will your job run? Where will the output of the date and who commands be sent?
+   6. In approximately one minute, type cat datefile and press Enter. View the output from your scheduled at job.
+   7. At the command prompt, type crontab -l and press Enter to list your cron table. Do you have one?
+   8. At the command prompt, type crontab -e and press Enter to edit a new cron table for the root user. When the vi editor appears, add the line:

```
30 20 * * 5 /bin/false
```