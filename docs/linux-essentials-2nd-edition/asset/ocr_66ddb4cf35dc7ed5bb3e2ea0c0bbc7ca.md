# Chapter 14 - Setting Ownership and Permissions

# THE ESSENTIALS AND BEYOND (Continued)

# REVIEW QUESTIONS

+   1. What command would you type (as root) to change the ownership of somefile.txt from ralph to tony?
   A. chown ralph:tony somefile.txt
   B. chmod somefile.txt
   C. chown somefile.txt tony
   D. chown tony somefile.txt
   E. chmod tony somefile.txt
2. Typing ls -ld wonderjaye reveals a symbolic mode of drwxr-xr-x. Which of the following are true? (Select all that apply)
   A. wonderjaye is a symbolic link.
   B. wonderjaye is an executable program.
   C. wonderjaye is a directory.
   D. All users of the system may read wonderjaye.
   E. Any member of the file's group may write wonderjaye.
3. Which of the following commands can you use to change a file's group?
   A. groupadd
   B. groupmod
   C. chmod
   D. ls
   E. chown
4. True or false: A file with permissions of 755 can be read by any user on the computer, assuming all users can read the directory in which it resides.
5. True or false: Only root may use the chmod command.
6. True or false: Only root may change a file's ownership with chown.
7. What option allows chosen to change ownership on an entire directory tree?
8. What three-character symbolic string represents read and execute permission but no write permission?
9. What symbolic representation can you pass to chmod to give all users execute access to a file without affecting other permissions?
10. You want to set the sticky bit on an existing directory, subdir, without altering its permissions. To do so, you would type chmod subdir.