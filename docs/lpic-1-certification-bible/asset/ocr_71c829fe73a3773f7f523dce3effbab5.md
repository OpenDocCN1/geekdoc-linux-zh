```
```
debian:~# read first last
lee johnson
debian:~# echo $first
lee
debian:~# echo $last
johnson
```
```

# # Script considerations

The security on shell scripts should be set correctly and checked often. If the scripts are stored in a world-readable location there can be serious security implications if the permissions are set incorrectly. If a nontrusted user can change a script file, they can modify its function to access data from any user that runs it. It is best never to set scripts to run SUID, as this can open very large security holes in any system.

# # Key Point Summary

The Linux environment can be greatly customized to suit your needs and tastes. You can combine the startup script files with the powerful shell scripting abilities, and if a function isn't built in, you can write your own easily.

+   - vi is a popular text mode editor that is installed by default on most Linux and UNIX systems.
+   - To open a file at line ten, use the syntax vi +10 filename.
+   - To open a file at the first instance of string, use the syntax vi /string filename.
+   - vi has three different modes: command, insert, and last line.
+   - To save a file in vi, use the :w command.
+   - To exit vi and save changes, use either ZZ or :wq.
+   - To close vi without saving changes, use the :q! command.
+   - The vi cursor movement keys are k for up, j for down, h for left, and l for right.
+   - Most commands can be repeated by preceding them with a number.
+   - To insert text in vi, use the i command.
+   - To append text in vi, use the a command.
+   - To create a new line in vi, use either the o or O commands.
+   - To change text in vi, use either the c or C commands.
+   - To replace text in vi, use either the r or R commands.
+   - To delete text in vi, use either the x or X commands.