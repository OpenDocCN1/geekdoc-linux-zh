# HANDS-ON PROJECTS

# Project 5-1

In this project, you use several basic filtering commands to modify a text file. To complete this project you should have a working Linux system with a valid user account. This project should work on any version of Linux with a standard utility set.

+   1. Log in to Linux using your user name and password.
+   2. If you are using a graphical environment, open a terminal window so you have a shell prompt.
+   3. Use the following command to copy the /etc/passwd file to your home directory as a test file named data1 (we use this file because it has lines that are separated into fields):
+      `cp /etc/passwd ~/data1`
+   4. Make sure you are working in your home directory by typing:
+      `cd`
+   5. Use this command to look at your working file to see how it is organized and formatted:
+      `less data1`
+   6. Each line in this file is divided into fields using a colon. Press q to exit the less command. Now use the cut command as shown below to extract from each line the first and seventh fields (the user name and associated default shell):
+      `cut -d : -f 1,7 data1 > data2`
+   7. Review the contents of data2 using the less command as shown here:
+      `less data2`
+   8. Press q to exit the less command. Convert the colon (:) character between the remaining two fields of each line of data2 to a tab character using the tr command as shown here and store the result in data3:
+      `tr ":" "\t" < data2 > data3`
+   9. Use the following command to sort the lines in the data3 file into alphabetical order and store the result in data4:
+      `sort data3 > data4`
+   10. You decide that you should have sorted the file in the opposite order. Reverse all the lines in the data4 file using the tac command as shown below, and store the results in data5:
+       `tac data4 > data5`