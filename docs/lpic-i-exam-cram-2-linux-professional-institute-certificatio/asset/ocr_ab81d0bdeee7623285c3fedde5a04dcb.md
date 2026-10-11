To illustrate this, open the /etc directory in the vi editor and navigate from link to link, proving that the directory is a file that links from one place to another. Try it as shown here:

+   1.  Open a shell session as a normal user.

+   2.  Edit the /etc directory in vi with the following command:

```
vi /etc
```

You’ll see something like the following:

```
" Press ? for keyboard shortcuts
" Sorted by name (.bak,*,.O,.h,.info,.swp,.obj at end of list)
"= /etc/
../
CORBA/
X11/
aep/
alchemist/
alternatives/
amanda/
ata lk/
bonobo-activation/
cipe/
cron.d/
cron.daily/
```

+   3.  Place the cursor on the X11/ line and press the Enter key.

Notice that the directory changes to reflect your being in the /etc/X11/ directory.

![](bbox=[0.07, 0.6, 0.24, 0.7])

> If you navigate to a regular file and press Enter, you load that file and are unable to return to the higher directories. Doing this simply edits the file, just as if you had invoked the vi editor with that file as an argument.

+   4.  Navigate back to the /etc directory by pressing the Enter key while the cursor is on the .../ entry.

+   5.  For curiosity sake, when back in the /etc directory, choose the .../ entry and notice that you’re now in the root of the system.

It’s interesting to note that you can navigate the entire tree of the file system as one big file if you choose to.

+   6.  Exit the vi editor by typing :q! to ensure you didn’t make any changes.

Now you can see that the entire file system is like a big file that contains entries that point to other directory files or regular files.