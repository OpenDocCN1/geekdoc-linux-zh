not be displayed onscreen. Actually, nothing will be displayed onscreen. Don't worry, though. Your password is being read.

After you enter the password, the login program checks the password database for a match. If it finds one, you get a screen that looks something like this:

```
Last login: Tue Apr 10 15:19:17 on ttyp0
Copyright (c) 1980, 1983, 1986, 1988, 1990, 1991, 1993, 1994
	The Regents of the University of California. All rights reserved.

FreeBSD 5.0-RELEASE (GENERIC) #0: Sun Dec 8 15:17:26 CDT 2002

>
```

If this is the first time you log in with your normal user account, you probably won't see the first line, Last login. In the future when you log in, however, this line will be present.

> **CAUTION**
> It's a good idea to pay attention to the "last login" information. If, for example, FreeBSD says your last login was
> 
> Sat Sept 15 14:05:29
> 
> and you know you didn't log in to the system on that day, then someone else has logged in to your account. If something like this ever happens, you need to change your password immediately (use the passwd command and follow the instructions it gives). Also, be sure to notify your system administrator of the security breach (assuming you are not the system administrator). If you are the system administrator, see Chapter 29, "Network Security," for further information on what to do if you think your network has been compromised.

The rest of the screen shows copyright information as well as information about the kernel and when it was built. The final line is the shell prompt. When you see the shell prompt, FreeBSD is waiting for you to give it something to do.

> **CAUTION**
> Notice the difference between the command prompt you get this time and the command prompt you got last time (when you logged in as the root user). The root user's login prompt is the pound sign (#). A normal user's login prompt will usually be either $ for Bourne-style shells or % or > for C-style shells. The default shell in FreeBSD is tcsh, which is a C-style shell. Either way, the type of prompt you have serves as a constant reminder of whether you are logged in as root. If you are, be extra careful when issuing potentially dangerous commands.