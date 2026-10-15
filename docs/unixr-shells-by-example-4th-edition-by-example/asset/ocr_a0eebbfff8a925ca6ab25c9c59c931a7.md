# LAB 14: CONDITIONAL STATEMENTS

+   1. Write a script called checking that will do the following:
+      a. Take a command-line argument: a user's login name.
+      b. Test to see if a command-line argument was provided.
+      c. Check to see if the user is in the /etc/passwd file. If so, it will print Found <user> in the /etc/passwd file.
+      d. Otherwise, it will print No such user on our system.

+   2. In the lookup script, ask the user if he or she would like to add an entry to datafile. If the answer is yes or y:
+      a. Prompt the user for a new name, phone, address, birth date, and salary. Each item will be stored in a separate variable. You will provide the colons between the fields and append the information to datafile.
+      b. Sort the file by last names. Tell the user you added the entry, and show him or her the line preceded by the line number.

# LAB 15: CONDITIONALS AND FILE TESTING

+   1. Rewrite checking. After checking whether the named user is in the /etc/passwd file, the program will check to see if the user is logged on. If so, the program will print all the processes that are running; otherwise, it will tell the user <user> is not logged on.

+   2. The lookup script depends on datafile to run. In the lookup script, check to see if the datafile exists and if it is readable and writable. Add a menu to the lookup script to resemble the following:
+      [1] Add entry.
+      [2] Delete entry.
+      [3] View entry.
+      [4] Exit.
+      a. You already have the Add entry part of the script written. The Add entry routine should now include code that will check to see if the name is already in datafile and if it is, tell the user so. If the name is not there, add the new entry.
+      b. Now write the code for the Delete entry, View entry, and Exit functions.
+      c. The Delete part of the script should first check to see if the entry exists before trying to remove it. If it does not exist, notify the user; otherwise, remove the entry and tell the user you removed it. On exit, make sure that you use a digit to represent the appropriate exit status.
+      d. How do you check the exit status from the command line?