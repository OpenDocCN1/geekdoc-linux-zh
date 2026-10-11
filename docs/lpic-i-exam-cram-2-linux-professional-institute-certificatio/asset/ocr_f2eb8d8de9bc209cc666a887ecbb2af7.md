Table 2.4 Special Characters for the Prompt (continued)
| Code | Will Display |
|---|---|
| \! | The history number of this command. |
| \# | The command number of this command. |
| \$ | If the effective UID is 0, it's a #; otherwise, it's a $. |
| \n.nn | The character corresponding to the octal number nn. |
| \\ | A backslash. |
| \[ | Begin a sequence of nonprinting characters, which could be used to embed a terminal control sequence into the prompt. |
| \] | End a sequence of nonprinting characters. |

# ## Configuring the Prompt Step by Step

Let's change the prompts by editing the various files and causing the prompts to take effect:

+   1. As the root user, edit the `/etc/bashrc` file with the following:
+      `vi /etc/bashrc`
+   2. Press the G key to navigate to the end of the file.
+   3. Add another line at the bottom of the file by pressing the O key.
+   4. Enter the following prompt information in your new line:
+      `PS1="[\u@\h  global \W]\$"`
+   5. Press the Esc key to go back to command mode.
+   6. Save and exit the file by typing :wq.
+   7. Switch to terminal (tty2) number 2 by pressing Alt+F2.
+   8. Log in as a non-root user. The global test should appear in the prompt.
+   9. Switch back to tty1 by pressing Alt+F1; then run the following command to reread the /etc/bashrc configuration file for the root user:
+      `. /etc/bashrc`
+      The command starts with a period and then the full path to the /etc/bashrc file.
+   10. The settings should be refreshed. You could have also used the following command:
+      `source /etc/bashrc`