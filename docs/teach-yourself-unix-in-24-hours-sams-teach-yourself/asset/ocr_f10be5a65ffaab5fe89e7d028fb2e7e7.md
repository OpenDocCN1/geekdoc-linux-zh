Either way, you can now try vi again, and it should work.

If it does work, append the command (whichever of these two commands was successful for you) to your .login file if you use csh or to .profile if you use sh or ksh. You can do this by entering whichever of the following commands is appropriate for your system:

```
% echo setenv TERM vti100 >> .login
```

or

```
$ echo "TERM=vti100; export TERM" >> .profile
```

This way, the next time you log in, the system will remember kind of terminal you're using.

![](bbox=[0.165, 0.365, 0.285, 0.452])

vi and other screen commands use a UNIX package called curses to control the screen. Like most UNIX applications, curses was not designed for a specific configuration; instead, it was designed to be device-independent. Therefore, to work on a specific device, you need to give it some additional information—in this case, the terminal type.
If vt100 didn't work, it is to talk to your system administrator about the problem or call your UNIX vendor to find out what the specific value should be. If you are connected through a modem or other line and you are actually using a terminal emulator or communications package, you might also try using that as a TERM setting. If that fails, call the company that makes your software and ask the company what terminal type the program expects.

+   3. Great! You have successfully launched vi, see what it looks like, and even entered
t most important command: the quit command. Now create a simple file and
start vi it shows you the contents of the file:

```
% ls -l demo
% vi demo
```

| total 29 | 2 taylor | 512 Nov 10:39 Archives/ |
| drwx------ | 3 taylor | 512 Dec 02:03 Infolist/ |
| drwx------ | 2 taylor | 1024 Dec 03:014 Mail/ |
| drwx------ | 2 taylor | 512 Oct 06:39 News/ |
| drwx------ | 4 taylor | 512 Dec 22:08 OWL/ |
| drwx-rw-- | 1 taylor | 126 Dec 3 16:34 awkscript |
| -rw-rw-- | 1 taylor | 165 Dec 3 16:42 bigfiles |
| drwx------ | 2 taylor | 512 Oct 13 10:45 bin/ |
| -rw-rw-- | 1 taylor | 0 Dec 3 22:26 demo |

![](bbox=[0.065, 0.832, 0.145, 0.962])