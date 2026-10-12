+   4. Next, you need to prepare the dictionary files that Crack will use when trying to guess passwords. Do that with the following command:

```
# ./Crack -makedict
```

# ## Running the Crack command

Crack is now ready to run. Before you can run it, however, you must make your password file available in a format that Crack can read. The easiest way to do this is to run the shadmgr.sv script provided with Crack. You must be running as root to run the script, so use the su command to assume root privilege. The shadmgr.sv script is in the scripts directory within the primary Crack directory. It prints the merged password data to the screen, so you will need to redirect the output to a file when you invoke the command:

```
# ./scripts/shadmgr.sv > mypasswd
```

You should now be back at a command prompt. The new mypasswd file should be in the current directory. Unfortunately, it is still owned by root, and unless you plan to run Crack as root, you will need to change this. Type the following commands, replacing myname with your actual login name:

```
# chown myname mypasswd
# chmod 600 mypasswd
```

The chown command modifies the file so that it is owned by you rather than by root. (Replace myname with your user name.) The chmod command changes the file permissions so that only you can read it. THIS IS EXTREMELY IMPORTANT! You must change the permissions on this file so it is readable only by you; otherwise, you are opening a security hole on your system. If the file is readable by other users on the system, they can copy the file and then run Crack against it themselves.

Finally, exit the root shell using the exit command, and then run Crack against the merged password file using the following command:

```
# ./Crack mypasswd
```

This will start up the password cracking process, put it into the background, and return you to a command prompt. This does not mean that Crack is already done. Cracking a password file can take hours or even days depending on the size of the file. Crack will work on the file in the background and automatically exit when finished. You can pause, stop, or check the progress of Crack at any time. Table 14-3 lists the command lines that you are likely to find useful.