Now, if you use the pwd command, that command shows /usr/share/doc/bash-2.04 as the current directory. Therefore, you can refer to a directory's name in two ways:

+   - An absolute pathname (such as /usr/share/doc) that specifies the exact directory in the directory tree
+   - A relative directory name (such as bash-2.04, which represents the bash-2.04 subdirectory of the current directory)

If you type cd bash-2.04 in /usr/share/doc, the current directory changes to /usr/share/doc/bash-2.04. However, the same command in /home/naba tries to change the current directory to /home/naba/bash-2.04, which probably does not exist. Incidentally, typing the cd command without any arguments changes the current directory to your home directory.

![](bbox=[0.07, 0.4, 0.2, 0.49])

You can use a shortcut to refer to any user's home directory. Prefix a user's login name with a tilde (~) to refer to that user's home directory. Therefore, ~naba refers to the home directory of the user naba and ~root refers to the home directory of the root user. If your system has a user with the login name emily, you can type cd ~emily to change to Emily's home directory.

The directory names . and .. have special meanings. A single period (.) indicates the current directory, whereas two periods (..) indicate the parent directory. If the current directory is /usr/share/doc, for example, you can change the current directory to /usr/share by typing this command:

```
cd ..
```

Essentially, this command takes you up one level in the file system hierarchy.

# Directory listings and permissions

As you move around the Linux directories, you may want to know the contents of a directory. You can get a directory listing by using the ls command. By default, the ls command — without any options — displays the contents of the current directory in a compact, multicolumn format. For example, type the following commands to see the contents of the /etc/X11 directory. (Type the commands shown in boldface; I omitted the command prompts from the listing.)

```
cd /etc/X11
ls
```