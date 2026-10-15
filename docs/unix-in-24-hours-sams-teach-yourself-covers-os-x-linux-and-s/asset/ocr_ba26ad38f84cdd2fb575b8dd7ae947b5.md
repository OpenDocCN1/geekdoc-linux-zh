directory, Unix knows that execute permission is important, and so it grants it. However, for data files (particularly text files), execute permission doesn’t make sense, so the particular program creating the file (the shell, an editor, the email system, etc.) actually skips it, regardless of the umask setting.

Another way to look at this is that any time you create a file containing information, the original mask that the system uses to compare against your umask is not 777 (not rwxrwxrwx, to put it another way) but rather 666 (rw-rw-rw-). This is in recognition of the unlikely case that you’ll want to mark the new file as executable.

The good news is that you now know an easy way to set the execute permission for a file if the system gets it wrong: chmod +x filename does the trick.

+   1. Turn to your computer and check your umask setting and then alternate between changing its values and creating new files with touch:

Click here to view code image

```
% umask
0007
% touch test.07
% ls -l test.07
-rw-rw-- 1 taylor 0 Oct 12 14:38 test.07
```

+   2. To change the value of your umask, add the numeric value of the desired mask to the command line:

```
% umask 077
```

This changes my umask value from 007 (------rwx, which produces a 770 default permission: rwxrwx---) to 077 (---rwxrwx, which produces a 700 default permission: rwx------). Before you look at the following output, what would you expect this modification to mean? Remember that you should read it as exactly the opposite of how you want the default permissions:

Click here to view code image

```
% touch test.077
% ls -l test.077
-rw--- 1 taylor 0 Oct 12 14:38 test.077
```

Is that what you expected?

+   3. What would you have as your umask if you want to have the default permission keep files private to just the owner and make them read-only?

You can work through this problem in reverse. If you want r-x------ as the default permission (because the system takes care of whether execute permission is needed, based on file type), write down the opposite permission, which is -w-rwxrwx. Translate that to a binary number, 010 111 111, and then to a three-digit value, 277 (010 = 2, 111 = 7, 111 = 7). That’s the answer. The value 277 is the correct umask value to ensure that files you create are read-only for yourself and off-limits to everyone else:

Click here to view code image

```
% umask 277
```