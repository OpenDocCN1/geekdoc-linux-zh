# Question 4

One of your Linux administrators has forgotten his root password on his Linux computer. Which of the following answers is the easiest way for him to set up a new password?

+   - a. Start Linux. Go into the CLI. Look through the /etc/inittab file to find the run level associated with single-user mode. Go into that mode with the init command, and restore a backup of the original /etc/passwd file.
+   - b. Boot your computer. When you see the LILO boot: prompt, enter the linux single command. When Linux starts, run the passwd command to set a new password for the root user.
+   - c. Boot your computer with your Linux installation CD. Select the applicable upgrade option. When prompted, enter new passwords for the root and other users on that computer.
+   - d. Boot your computer. When you see the LILO boot: prompt, enter the single command. When Linux starts, run the passwd command to set a new password for the root user.

![](bbox=[0.8, 0.17, 0.92, 0.3])

Answer b is correct. The linux single command, when entered at the LILO boot prompt, starts Linux in single-user mode. Your administrator can then use the passwd command to set up a new password for the root user. Only the root user can run the init command; because your administrator has forgotten his root password, the option shown in answer a is not possible. Although you can upgrade Linux and set up new passwords for all users, it is not the easiest thing to do, especially if the administrator is the only person who has lost his password. Therefore, answer c is incorrect. Unless your administrator has set up single as an option in the lilo.conf file, answer d will not start any mode of Linux and is therefore not correct.