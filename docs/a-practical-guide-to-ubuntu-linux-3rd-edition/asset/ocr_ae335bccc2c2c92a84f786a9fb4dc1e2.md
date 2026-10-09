a. Which error message do you get when you execute this script? Rewrite the script so that the error does not occur, making sure the output still goes to savehem.

b. What might be a problem with running this script twice in the same directory? Discuss a solution to this problem.

9. Read the bash man or info page, try some experiments, and answer the following questions:

a. How do you export a function?

b. What does the hash builtin do?

c. What happens if the argument to exec is not executable?

10. Using the find utility, perform the following tasks:

a. List all files in the working directory and all subdirectories that have been modified within the last day.

b. List all files that you have read access to on the system that are larger than 1 megabyte.

c. Remove all files named core from the directory structure rooted at your home directory.

d. List the inode numbers of all files in the working directory whose filenames end in .c.

e. List all files that you have read access to on the root filesystem that have been modified in the last 30 days.

11. Write a short script that tells you whether the permissions for two files, whose names are given as arguments to the script, are identical. If the permissions for the two files are identical, output the common permission field. Otherwise, output each filename followed by its permission field. (Hint: Try using the cut utility.)

12. Write a script that takes the name of a directory as an argument and searches the file hierarchy rooted at that directory for zero-length files. Write the names of all zero-length files to standard output. If there is no option on the command line, have the script delete the file after displaying its name, asking the user for confirmation, and receiving positive confirmation. A -f (force) option on the command line indicates that the script should display the filename but not ask for confirmation before deleting the file.