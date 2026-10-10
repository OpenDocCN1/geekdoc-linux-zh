+   22. At the command prompt, type `chmod u+x myscript4` and press Enter. Next, type `./myscript4` at the command prompt and press Enter. Were the permissions changed to rwx---- for myscript, myscript2, and myscript3?

+   23. Type `exit` and press Enter to log out of your shell.

# # Discovery Exercises

+   1. Name the command that can be used to do each of the following:
+      a. Create an alias called mm that displays only those file systems that are mounted and contain an ext4 file system.
+      b. Create and export a variable called NEWHOME that is equivalent to the value contained in the HOME variable.
+      c. Find all files that start with the word “host” starting from the /etc directory and save the Standard Output to a file called file1 and the Standard Error to the same file.
+      d. Display only the lines from the output of the set command that have the word “bash” in them. This output on the terminal screen should be sorted alphabetically.
+      e. Display only the user name (first field) in the colon-delimited /etc/passwd file and save the output to a file called users in the current directory.

+   2. What would happen if the user executed the following commands?
+   
+   ```
+   cp /etc/hosts ~
+   cd
+   tr A <hosts | sort -r | pr -d >hosts
+   ```
+   
+   Explain the output.

+   3. Recall that only Standard Output can be sent across a pipe to another command. Using the information presented in this chapter, how could you send Standard Error across the pipe in the following command?
+   
+   ```
+   ls /etc/hosts /etc/h | tr h H
+   ```

+   4. Name the test statement that can be used to test the following scenarios:
+      a. The user has read permission to the /etc/hosts file.
+      b. The user has read and execute permission to the /etc directory.
+      c. The contents of the variable $TEST are equal to the string “success.”
+      d. The contents of the variable $TEST are numerically equal to the contents of the variable $RESULT.
+      e. The contents of the variable $TEST are equal to the string “success” and the file /etc/hosts exists.
+      f. The contents of the variable $TEST are equal to the string “success,” or the number 5, or the contents of the variable $RESULT.

![](bbox=[0.94, 0.37, 0.99, 0.44])