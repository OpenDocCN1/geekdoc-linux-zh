1. Turn to your computer and try using the numeric mode of chmod, along with ls, to display the actual permissions to learn for yourself how this works:

Click here to view code image

```
% touch example
% ls -l example
-rw-rw-- 1 taylor 0 Oct 12 10:16 example
```

By default, files are created in my directory with mode 660. This is determined by the umask setting, as we’ll explore shortly.

2. To take away read and write permission for people in my group, I’d replace the 660 permission with what numeric permissions string? I’d use 600:

Click here to view code image

```
% chmod 600 example
% ls -l example
-rw--- 1 taylor 0 Oct 12 10:16 example
```

3. What if I change my mind and want to open up the file for everyone to read or write? I’d use 666:

Click here to view code image

```
% chmod 666 example
% ls -l example
-rw-rw-rw- 1 taylor 0 Oct 12 10:16 example
```

4. Finally, pretend that the example is actually a directory. What numeric mode would I specify to enable everyone to use ls in the directory and enable only the owner to add or delete files? I’d use 755:

Click here to view code image

```
% chmod 755 example
% ls -l example
-rwxr-xr-x 1 taylor 0 Oct 12 10:16 example
```

You’ve looked at both the numeric mode and the symbolic mode for defining permissions. Having learned both, which do you prefer?

# Note

Somehow I’ve never gotten the hang of symbolic mode, so I almost always use the numeric mode for chmod. The only exception is when I want to add or delete simple permissions. Then, I use something like chmod +r test to add read permission. Part of the problem is that I don’t think of the user of the file but rather the owner, which puts me in mind of “o”—and specifying o+r causes chmod to change permission for others, not the owner. It’s important, therefore, that you remember that files have users so you remember u for user, and that everyone not in the group is other so you remember o. Otherwise, learn the numeric shortcut!

File permissions and modes are one of the most complex aspects of Unix. You can tell this because it’s taken two hours to explain it fully. It’s important that you spend the time to understand how the permissions strings relate to directory permissions, how to read the