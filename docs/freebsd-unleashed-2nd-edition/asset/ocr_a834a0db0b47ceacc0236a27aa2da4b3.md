```
# csh frank
#Changing user database information for frank.
Shell: /bin/tcsh
Full Name: Frank Allen
Office Location:
Office Phone:
Home Phone:
Other information:
-
-
```

A full discussion of how to use the vi editor is found in Chapter 6, “Working with Applications.” For now, let’s concentrate on the necessary commands you’ll need for changing the user’s shell.

Part of what makes vi so challenging is that its internal commands are so arcane and must be entered so exactly that it’s easy to get to a point at which crucial data has been acciden- tally deleted or mangled and can’t be retrieved. If you make a mistake, enter a colon ( : ), followed by q!, and then press Enter, which will force an exit without saving changes:

```
-
:
:q!
```

Let’s say you want to change frank’s shell permanently from /bin/tcsh to /usr/local/bin/bash. Once you’re in the vi screen, obtained by typing csh frank, use the arrow keys to move to the beginning of the word tcsh, immediately after the second slash ( / ). Type c (for “change”) and then w (for “word”). A dollar sign ($) will appear at the end of the word you’re changing:

```
Shell: /bin/tcsh$
```

Type bash in place of the word tcsh and then press Esc to exit change-word mode. Now the shell is /bin/bash. The next step is to place the cursor on top of the first slash, just before bin, and type i (for “insert”) to get a usable cursor. Enter /usr/local and then press Escape. The shell string should now be /usr/local/bin/bash.

Now, enter a colon (: ) to go into the in-program command line and then follow it with w (for “write”). Press Enter to save the file. Finally, type :q and press Enter to quit.

The file you’ve now written is actually a temporary file in /etc. If your changes are valid, they will be read from that file and automatically rebuilt into /etc/master.passwd and /etc/passwd. From now on, every time the user in question logs in to the system, the login will be under /usr/local/bin/bash rather than /bin/tcsh.