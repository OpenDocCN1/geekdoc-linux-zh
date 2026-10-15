# Creating Files with touch

Another skill you’ll use frequently is creating files. You might think of creating files as getting an empty bucket that you can later fill with water…or sand…or rocks…or whatever. When you create a file, you designate an empty space that you can fill with programs, activity logs, your resume, or configurations—practically anything you want, or nothing at all.

Of course, you can always create a file by writing something in an editor and saving it, as described in Chapter 4, but you will sometimes encounter situations where you just need an empty file as a placeholder for later use. You create empty files using the touch command, as shown in Code Listing 2.2.

# To create a file:

+   1. `touch file.to.create`
+   
+   To create a file, type touch followed by the name of the file. This creates an empty file.

```
$ ls
$ touch file.to.create
$ ls -l file*
-rw-rw-r- 1 ejr users 0 Jun 29 11:53 file.to.create
$ touch -t 12312359 oldfile
$ ls -l
total 0
-rw-rw-r- 1 ejr users 0 Jun 29 11:53 file.to.create
-rw-rw-r- 1 ejr users 0 Dec 31 1998 oldfile
$ touch -t 200312312359 new.years.eve
$ ls -l
total 0
-rw-rw-r- 1 ejr users 0 Jun 29 11:53 file.to.create
-rw-rw-r- 1 ejr users 0 Dec 31 2003 new.years.eve
-rw-rw-r- 1 ejr users 0 Dec 31 1998 oldfile
$
```

Code Listing 2.2 Use the touch command to create files, update their modification times, or both.