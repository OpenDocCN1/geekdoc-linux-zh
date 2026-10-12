```
lrwxrwxrwx  1 sheila  root  8 Feb  7 11:49 plan -> todo.txt
-rw-r--r--  1 sheila  root  21 Feb  7 11:41 todo.txt
```

The plan file is a symbolic link to todo.txt. Now, suppose the root user changes the ownership of the symbolic link as follows:

```
chown kabir plan
```

The ls -l output shows:

```
lrwxrwxrwx  1 kabir  root  8 Feb  7 11:49 plan -> todo.txt
-rw-r--r--  1 sheila  root  21 Feb  7 11:41 todo.txt
```

As you can see, the permissions of the plan symlink have changed from user sheila to user kabir, but todo.txt is still owned by sheila. As a result, kabir cannot write to todo.txt using the plan symbolic link unless the directory where these files are stored is owned by user kabir. However, if you change the permission settings of a soft link, the file that the soft link points to inherits the new settings. For example, the following command changes the todo.txt file's permission:

```
chmod 667 plan
```

Executing the ls -l command after executing the above permissions command results in the following output:

```
lrwxrwxrwx  1 kabir  root  8 Feb  7 11:49 plan -> todo.txt
-rw-rw-rwx  1 sheila  root  21 Feb  7 11:41 todo.txt
```

# Creating a permission policy

Most problems that users encounter on Unix and Unix-like systems are related to file permissions. If something that was working fine yesterday suddenly stops working, you should first suspect a permission problem. The following section discusses a few permission policies that you might want to implement, especially if you have many users on a single system, to keep permission snafus to a minimum.

![](bbox=[0.08, 0.93, 0.18, 0.99])

One of the most common causes of permission problems involves misuse of the root account. Many inexperienced