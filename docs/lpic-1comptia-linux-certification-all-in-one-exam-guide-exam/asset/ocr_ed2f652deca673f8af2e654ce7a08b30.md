![](bbox=[0.39, 0.09, 0.94, 0.42])

Notice in Figure 11-1 that there are actually two owners for contacts.odt. The first is the name of the user who owns the file. In this case, it’s ksanders. In addition, the users group owns the file as well. That’s because users is the primary group that ksanders belongs to.

You can also view file ownership from the command line using the `ls -1` command. This has been done in ksanders’ home directory in this example:

```
```
ksanders@wsl:~> ls -1
total 40
drwxr-xr-x 2 ksanders users 4096 2011-03-10 16:43 bin
-rw-r-- 1 ksanders users 0 2011-03-18 08:02 contacts.odt
drwxr-xr-x 2 ksanders users 4096 2011-03-10 16:44 Desktop
drwxr-xr-x 2 ksanders users 4096 2011-03-10 16:44 Documents
drwxr-xr-x 2 ksanders users 4096 2011-03-10 16:44 Downloads
drwxr-xr-x 2 ksanders users 4096 2011-03-10 16:44 Music
drwxr-xr-x 2 ksanders users 4096 2011-03-10 16:44 Pictures
drwxr-xr-x 2 ksanders users 4096 2011-03-10 16:44 Public
drwxr-xr-x 2 ksanders users 4096 2011-03-10 16:43 public_html
drwxr-xr-x 2 ksanders users 4096 2011-03-10 16:44 Templates
drwxr-xr-x 2 ksanders users 4096 2011-03-10 16:44 Videos
ksanders@wsl:~>
```
```

Notice that the third column in the output displays the name of the file or directory’s owner (ksanders) while the fourth column displays the name of the group that owns it (users). While file and directory ownership is automatically assigned at creation, it can be modified. Let’s discuss how this is done next.

# Managing Ownership from the Command Line

File and directory ownership isn’t a fixed entity. Even though ownership is automatically assigned at creation, it can be modified. You can specify a different user and/or group as the owner of a given file or directory. To change the user who owns a file, you