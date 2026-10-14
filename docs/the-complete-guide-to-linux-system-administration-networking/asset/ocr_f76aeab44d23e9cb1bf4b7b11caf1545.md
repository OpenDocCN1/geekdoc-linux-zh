+   4. List the shells that are installed on the system using the command ls *sh. Can you recognize all of the shells listed?
+   5. Change to the directory /etc using the command cd /etc.
+   6. Type the command ls -l host but don't press Enter.
+   7. Press the Tab key twice. The first time you press Tab the shell beeps. The second time it displays a list of files in /etc that begin with host.
+   8. Type s. (including the period, so that the command line contains ls -l hosts), but don't press Enter.
+   9. Press the Tab key twice. The shell beeps and then displays all the files in /etc that begin with hosts. (including the period). The list is shorter than the output of Step 7 because you added more characters to the search.
+   10. Type a and press Tab. The shell fills in the full file name so that the line reads ls -l hosts.allow.
+   11. Press Enter to complete the ls command that the Tab key finished filling in.
+   12. Change to your home directory by entering the command cd.
+   13. Enter the command ls to execute the most recently used ls command, which you entered in Step 11. Why does the command display an error now?
+   14. Enter the command echo $PS1 to display the format of the standard shell prompt.
+   15. Enter the command man bash to view the manual page for the bash shell.
+   16. Enter the text \W to search for the string \W, which is part of the PS1 value you saw in Step 14.
+   17. Use the arrow keys to review the list of parameters that you can use to redefine the PS1 environment variable. Locate the \d option.
+   18. Press q to exit the man page viewer.
+   19. Enter the command export PS1="\d$PS1". What happened? What does the $PS1 at the end of the command indicate?
+   20. Enter the command bash to start a new shell. How does the shell prompt change? Why?
+   21. Enter the exit command to leave the new shell you started in Step 20. Then enter exit again to close the shell you have been working in since Step 2.
+   22. Open a new shell. What does the prompt look like? Why? Close the shell and log off.