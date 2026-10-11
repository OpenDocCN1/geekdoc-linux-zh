+   2. Extend ch05-catdir.c to call stat() on each file name found. Then print the inode number, the result of fmt_mode(), the link count, and the file’s name.

+   3. Extend ch05-catdir.c further such that if a file is a symbolic link, it will also print the name of the pointed-to file.

+   4. Add an option such that if a filename is that of a subdirectory, the program recursively enters the subdirectory and prints information about the subdirectory’s files (and directories). Only one level of recursion is needed.

+   5. If you’re not using a GNU/Linux system, run ch05-trymkdir (see Section 5.2, “Creating and Removing Directories,” page 130) on your system and compare the results to those we showed.

+   6. Write the mkdir program. See your local mkdir(1) manpage and implement all its options.

+   7. In the root directory, /, both the device and inode numbers for ‘.’ and ‘..’ are the same. Using this bit of information, write the pwd program.

The program has to start by finding the name of the current directory by reading the contents of the parent directory. It must then continue, working its way up the filesystem hierarchy, until it reaches the root directory.

Printing the directory name backwards, from the current directory up to the root, is easy. How will your version of pwd manage to print the directory name in the correct way, from the root on down?

+   8. If you wrote pwd using recursion, write it again, using iteration. If you used iteration, write it using recursion. Which is better? (Hint: consider very deeply nested directory trees.)

+   9. Examine the rpl_ufime() function (see Section 5.5.3.1, “Faking utime(file, NULL),” page 159) closely. What resource is not recovered if one of the tests in the middle of the l: f fails? (Thanks to Geoff Collier.)

+   10. (Hard.) Read the chmod(1) manpage. Write code to parse the symbolic options argument, which allows adding, removing, and setting permissions based on user, group, other, and “all.”

Once you believe it works, write your own version of chmod that applies the permission specification to each file or directory named on the command line. Which function did you use, chmod()—or open() and fchmod()—and why?