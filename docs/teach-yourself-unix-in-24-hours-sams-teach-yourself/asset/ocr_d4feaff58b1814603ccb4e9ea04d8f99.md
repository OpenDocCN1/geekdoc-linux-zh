# Ownership and Permissions

This time UNIX searched through my search path, found a file that matched the name of the program I requested, and then ascertained that it wasn't executable.
The resultant error message: Permission denied.

+   3. Now try entering -hi on your computer system. You'll get a different error message, Command not found, which tells you that UNIX searched all the directories in your search path but couldn't find a match.

+   4. Check your PATH and find a directory that you can add files in. You'll probably have a bin directory in your home directory, as I have /users/tail/bin in my search path. That's a good place to add a file using the touch command:

```
% env PATH
/users/tail/bin:bin:/usr/ucb:/usr/local:/usr/local/bin:
% touch my.new.cmd
% ls -l bin
-rw-r---- 1 taylor 0 Oct 11 15:07 my.new.cmd
```

+   5. Now try to execute the command by entering its name directly:

```
% my.new.cmd
/users/tail/bin/my.new.cmd: Permission denied.
```

![](bbox=[0.125, 0.483, 0.198, 0.535])

> If you're using the C Shell as your interpreter, it probably won't find the new command you created. This is because, to speed things, it keeps an internal table of different commands are found in your search path. You need to force the program to rebuild its table, and you can do that with the simple command rehash. If, when you enter the filename, don't get permission denied but instead see Command not found, enter rehash and try again.

JUST A MINUTE

+   6. Finally, use chmod to add permission to the file, and try it one more time.

```
% chmod +x bin/my.new.cmd
% ls -l bin/my.new.cmd
-rw-r--r-- 1 taylor 0 Oct 11 15:07 my.new.cmd
% my.new.cmd
```

Voila! You've created your first command, an achievement even though it doesn't do much. You can now see the search path and the UNIX philosophy of having applications identical to regular files, except for the permission, can be invaluable as you learn to customize your environment.

![](bbox=[0.125, 0.863, 0.198, 0.893])

SUMMARY

Execute permission enables the user to run the file as if it were a program. Execute permission is independent of other permissions granted—or denied—so it's perfectly feasible to have a program with read and execute permission, but no write permission.(After all, you wouldn't want others altering the program itself.) You also can have programs with

5