is for special permissions, discussed next). The two mean new files will have the write privilege removed for members of the files group and other.

You can view your umask by simply typing the umask command or change it by using

```
umask newmask
```

You can also use umask with the same letter syntax as chmod by using the -S parameter (for Symbolic). It will also accept letters to set the mask. Using letters tells the system which bits to set, as opposed to which bits NOT to set for the number representation, which may be less confusing to use.

To make a change permanent, you can add the command on your shell startup script, so it gets run every time you start a shell.

# EXERCISE 10.3: Using umask

In this exercise, you'll see a quick use of umask.

+   1. mkdir test to create a test subdirectory.
+   2. umask to show the current mask -- probably 0022.
+   3. touch test_file1 to create a file.
+   4. ls -1 test_file1 to see the file mode.
+   5. umask 0000 to change the mask.
+   6. touch test_file2 to create a new file, using the changed mask.
+   7. ls -1 to compare the mode of your two files.

# Special Permissions

In addition to the normal permission bits, there are additional special permissions that are represented by a fourth octal number, put in front of the normal three. Linux figures out what you want automatically -- if you use four numbers, it understands the first one is for special permissions and if there are only three numbers, it sticks with the regular read, write, and execute permissions.

Similar to the normal permissions, an octal value of 4 is the setuid, 2 is the setgid, and 1 sets the sticky bit. They are set using the same chmod command as the normal bits, either using a four-digit octal value or the same method using letters, but with the following additional letters:

+   * s sets the user or group ID
+   * s restricted deletion flag
+   * t sticky bit