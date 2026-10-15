
## Changing Permissions with chmod

Suppose you've been working on a file called rowyourboat and you want to have your coworkers down the stream review it. To do so, you'll need to give other people permission to access the document. You can either give people in specific groups access or give everybody on the Unix system access. In particular, you can specify permissions for u(ser—that's you), g(roup), o(thers), and a(ll).

In addition to specifying permissions, you can also specify how much access a person or group can have to your file. For example, you can specify r(ead), w(rite), and (e)x(ecute) access, depending on how much you trust them not to ruin your rowyourboat masterpiece.

As shown in Code Listing 5.7, your first step is to check out what the current permissions are. Then, you can set permissions, add to them, or remove them as necessary.

### To check current permissions:

- ls -l r*

To begin, type ls -l r* to get a long listing of rowyourboat in the current directory. Code Listing 5.7 shows that the permissions are -rwxr-x--. This is actually three sets of permissions:

- For the user (rwx, in this example)
- For the group (r-x, here)
- For the world (---, here)

In this example, the user has read, write, and execute permissions; the group has only read and execute permissions; and all other users have no permissions.

```
[ejr@hobbes permissions]$ ls -l r*
-rwxr-x-- 1 ejr users 152779 Jul 24 15:10 rowyourboat
[ejr@hobbes permissions]$
```

Code Listing 5.7 Use ls -l to see the permissions on files.

### To set permissions:

chmod u=rwx,g=rx,o=r row*
Type chmod and specify who has access. In this case users have read, write, and execute permissions; the group has read and execute permissions; and others have read permission for all files in the directory that start with row (Code Listing 5.8).
The equals sign (=) specifies that the permissions granted in the command are the only permissions that apply. Any previous permissions will be removed.
The wildcard expression here (row*) specifies that the command applies to all files and directories that start with "row" in the current directory.

```
[ejr@hobbes permissions]$ ls -l
total 332
-rw-rw-r-- 1 ejr users 24850 Jul 24 14:59 black
-rw-r--r-- 1 ejr users 152779 Jul 24 15:10 rowyourboat
-rw-r--r-- 1 ejr users 128889 Jul 24 14:33 sage.sayings
-rw-rw-r-- 1 ejr users 23890 Jul 24 14:33 sayings
[ejr@hobbes permissions]$ chmod u=rwx,g=rx,o=r row*
[ejr@hobbes permissions]$ ls -l
total 329
-rwxr-xr-- 1 ejr users 24850 Jul 24 14:59 black
-rwxr-xr-- 1 ejr users 152779 Jul 24 15:10 rowyourboat
-rwxr-xr-- 1 ejr users 128889 Jul 24 14:33 sage.sayings
-rwxr-xr-- 1 ejr users 23890 Jul 24 14:33 sayings
[ejr@hobbes permissions]$
```

Code Listing 5.8 You can set permissions to ensure that all files have equivalent permissions.

### To add permissions:

```
chmod g+w rowyourboat
```

At the shell prompt, enter chmod, followed by

- The category. In this case, we've used g, for group, but you could also use o for others...or, of course, u for user, but you already have that access. You could also use a for all users (which includes u, g, and o).
- A plus sign indicates that you're adding the permission to the existing permissions, rather than setting absolute permissions.
- The permissions to grant. Here, we've used w, for write permission, but you could also use r for read or x for execute permissions, as your needs dictate.
- The filename (rowyourboat)

### To remove permissions:

```
chmod go-w rowyourboat
```

At the shell prompt, use chmod go-w plus the filename to remove write permissions for everyone except you, the file's owner. Note that we handled both group and other in a single command this time, although we could have used chmod g-w rowyourboat and chmod o-w rowyourboat to accomplish the same thing.

## Tips

- You can also use the -R flag with chmod to recursively apply the changes you make to permissions to all files and subdirectories in a directory. For example, chmod -R go-rwx * revokes all permissions from everyone except the user for all files in the current directory, all subdirectories in the current directory, and all files in all subdirectories.
- There are about a million and one ways to express permissions. For example, you could use chmod ugo= * (note the space before the *) or chmod u-rwx,g-rwx, o-rwx * to revoke all permissions from all files in the directory. (Note that you'll have to add your own permissions back to the files before you can do anything with them, if you try this out.)
- If you want to change permissions for multiple files, either use a wildcard expression or separate the filenames with commas (but no spaces).
