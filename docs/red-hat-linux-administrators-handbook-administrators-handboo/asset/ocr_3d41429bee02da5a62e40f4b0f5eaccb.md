```
-rw-r--r--  2 Sheila  root  21 Feb  7 11:41 plan
-rw-r--r--  2 Sheila  root  21 Feb  7 11:41 todo.txt
```

The chown command changed the ownership of plan, but the ownership of todo.txt (the original file) has also changed. So, when you change the ownership or permissions of a hard link, the effect also applies to the original file.

# Changing permissions or ownership of a soft link

Changing the ownership of a soft link, or symbolic link, does not work the same way as it does for a hard link. For example, take a look at the following ls -l output:

```
lrwxrwxrwx  1 sheila  root  8 Feb  7 11:49 plan -> todo.txt
-rw-r--r--  1 sheila  root  21 Feb  7 11:41 todo.txt
```

The plan file is a symbolic link for todo.txt. Now, suppose the root user changes the ownership of the symbolic link as follows:

```
chown kabir plan
```

The ls -l output shows:

```
lrwxrwxrwx  1 kabir  root  8 Feb  7 11:49 plan -> todo.txt
-rw-r--r--  1 sheila  root  21 Feb  7 11:41 todo.txt
```

The question now is whether user kabir can write to todo.txt using the symbolic link (plan). The answer is no, unless the directory where these files are stored is owned by kabir. So, changing a soft link's ownership does not work in the same way as with hard links. However, if you change the permission settings of a soft link, the file it points to gets the new settings. For example,

```
chmod 666 plan
```