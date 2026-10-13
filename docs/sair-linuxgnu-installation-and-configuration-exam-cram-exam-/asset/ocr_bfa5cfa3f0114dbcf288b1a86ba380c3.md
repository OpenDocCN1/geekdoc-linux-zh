# Practice Questions

# Question 1

Which of the following commands deletes all of your Linux files without prompting you?

+   a. rm -i * \
+   b. rmdir -r / home/mj/tmp
+   c. rm -rf / home/mj/tmp
+   d. rm -v * /home/mj/tmp

Answer c is correct. Remember to read these command options carefully! Because there is a space between the first forward slash (/) and home/mj/tmp, this rm command first removes all files and directories in your root (/) directory. The rm -i command prompts you before deleting files, so answer a is incorrect. Because there is no -r switch for the rmdir command, answer b is incorrect. Although the rm -v * /home/mj/tmp command first deletes all files in your current directory before deleting all files in the /home/mj/tmp directory, it does not delete all of your Linux files. Therefore, answer d is incorrect.

# Question 2

What is the purpose of the w command?

+   a. There is no purpose; there are no single-letter bash commands.
+   b. Lists currently logged on users.
+   c. Lists currently active programs.
+   d. Used as a general manual.

Answer b is correct. The w command, like who, lists all currently logged on users. Because w is a command, answer a is incorrect. The ps utility lists currently active programs, so answer c is incorrect. Because the man command calls out the manual for specific commands, answer d is incorrect.