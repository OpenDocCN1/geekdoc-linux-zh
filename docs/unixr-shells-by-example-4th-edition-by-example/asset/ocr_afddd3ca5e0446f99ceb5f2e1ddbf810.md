3. Write a program called dusage that will mail a list of users, one at a time, a listing of the number of blocks they are currently using. The list of users will be in a file called potential_hogs. One of the users listed in the potential_hogs file will be admin.

+   a. Use file testing to check that the potential_hogs file exists and is readable.
+   b. A loop will be used to iterate through the list of users. Only those users who are using over 500 blocks will be sent mail. The user admin will be skipped over (i.e., he or she does not get a mail message). The mail message will be stored in a here document in your dusage script.
+   c. Keep a list of the names of each person who received mail. Do this by creating a log file. After everyone on the list has been sent mail, print the number of people who received mail and a list of their names.

# LAB 61: FUNCTIONS

+   1. Rewrite the systype program from Lab 59 as a function that returns the name of the system. Use this function to determine what options you will use with the ps command in the checking program.
+   
+   The ps command to list all processes on AT&T UNIX is
+   ps -ef
+   
+   On UNIX/BSD UNIX/Linux, the command is
+   ps -aux or ps aux

2. Write a function called cleanup that will remove all temporary files and exit the script. If the interrupt or hangup signal is sent while the program is running, the trap command will call the cleanup function.

3. Use a here document to add a new menu item to the lookup script to resemble the following:
[1] Add entry
[2] Delete entry
[3] Change entry
[4] View entry
[5] Exit

Write a function to handle each of the items in the menu. After the user has selected a valid entry, and the function has completed, ask if the user would like to see the menu again. If an invalid entry is entered, the program should print
Invalid entry, try again.
and the menu will be redisplayed.