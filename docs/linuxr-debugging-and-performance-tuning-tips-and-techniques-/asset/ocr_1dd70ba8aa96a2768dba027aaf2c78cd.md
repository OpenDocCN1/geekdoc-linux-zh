+   9.  Enhance your `chown` to allow numeric user or group numbers, as well as names.
+   10. Write functions to copy user and group structures, including pointed-to data. Use `malloc()` to allocate storage as needed.
+   11. Write a specialized user-lookup library that reads the entire user database into a dynamically allocated array. Provide *fast* lookup of users, by both user ID number and name. Be sure to handle the case in which a requested user isn't found.
+   12. Do the same thing for the group database.
+   13. Write a `stat` program that prints the contents of the `struct stat` for each file named on the command line. It should print all the values in human-readable format: `time_t` values as dates and times, `uid_t` and `gid_t` values as the corresponding names (if available), and the contents of symbolic links. Print the `st_mode` field the same way as `ls` would.
+   
+   Compare your program to the GNU Coreutils `stat` program, both by comparing outputs and by looking at the source code.