functional system. You can also see the purpose of checking the executable permission status. I’m going to jump ahead a bit to show you one use of the chmod (change mode/permission) program so that you can see what happens if I remove the execute permission from the say.hi program with the -x flag:

Click here to view code image

```
% chmod -x bin/say.hi
% ls -l bin/say.hi
-rw-rw-- 1 taylor 9 Oct 11 13:32 bin/say.hi
% say.hi
/home/taylor/bin/say.hi: Permission denied.
```

This time Unix searched through my search path, found a file that matched the name of the program I requested, and then ascertained that it wasn’t executable. The resultant error message was Permission denied.

+   3. Now try entering say.hi on your computer system. You’ll get a different error message, Command not found, which tells you that Unix checked all the directories in your search path but couldn’t find a match anywhere.

+   4. Check your PATH and find a directory that you can add files in. You’ll probably have a bin directory in your HOME directory (for example, I have /home/taylor/bin in my search path). If you don’t, use mkdir bin to create one. It’s a good place to add a file using the touch command:

Click here to view code image

```
% echo $PATH
/home/taylor/bin:/bin:/usr/bin:/usr/ucb:/usr/local:/usr/local/bin:
% touch bin/my.new.cmd
% ls -l bin
-rw-rw-- 1 taylor 0 Oct 11 15:07 my.new.cmd
```

+   5. Now try to actually execute the command by entering its name directly:

Click here to view code image

```
% my.new.cmd
/home/taylor/bin/my.new.cmd: Permission denied.
```

# Note

If you’re using the C shell (instead of bash) as your command interpreter, as might be the case on FreeBSD, it probably won’t find the new command you just created. This is because, to speed things up, it keeps an internal table of where different commands are found in your search path. You need to force the program to rebuild its table, and you can do that with the simple command rehash. If, when you enter the filename, you don’t get a permission denied error but instead see Command not found, enter rehash and try again.

+   6. Finally, use chmod to add execute permission to the file and try executing it one more time:

Click here to view code image

```
% chmod +x bin/my.new.cmd
```