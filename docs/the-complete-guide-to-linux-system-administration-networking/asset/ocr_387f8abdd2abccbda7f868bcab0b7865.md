+   23. Press the letter o to change to insert mode on a new line below the current line.
+   24. Type your name.
+   25. Press Esc to return to command mode.
+   26. Type :wq and press Enter to save your file and exit vi. Close the shell and log off.

# Project 3-4

In this project, you use redirection operators to change the default flow of information between programs and files. To complete this project you should have a working Linux system with a valid user account.

+   1. Log in to Linux using your user name and password.
+   2. If you are using a graphical environment, open a terminal window so you have a shell prompt.
+   3. Create two files, each containing one line of text using these commands:
+      echo "Test file 1" > file1
+      echo "Test file 2" > file2
+   4. View the contents of the first file you created, using this command:
+      cat file1
+   5. Append the contents of file1 to file2, then view file2 by using the following commands:
+      cat file1 >> file2
+      cat file2
+   6. Execute the ls command for the /etc directory, sorting the resulting list of files and storing it in a file named etc_files in your home directory as shown:
+      ls /etc | sort > etc_files
+   7. View the contents of the etc_files file by using the following command. Press q to exit the less command.
+      cat etc_files | less
+   8. View the contents of the etc_files file again using this command:
+      less etc_files
+   The less program checks to see if there is input from the STDIN channel, as in Step 7. If so, less uses that input to operate on. If there is no input, then less checks for a file name on the command line that started the program, using the data in that file to operate on. Press q to exit the less command.