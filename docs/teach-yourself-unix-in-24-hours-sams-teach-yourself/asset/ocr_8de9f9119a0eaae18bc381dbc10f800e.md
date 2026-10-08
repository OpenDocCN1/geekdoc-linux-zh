# Creating, Moving, Renaming, Deleting Files and Directories

2. To create a directory, you need to specify what you'd like to name the directory and where you'd like to locate it in the file system (the default location is your current working directory):

```
% mkdir NEWDIR
% Is
Archives/
InfoWorld/
LISTS/
Mail/
NEWDIR/
% News/
mailing.lists.bitnet.Z
% OWL/umors.26Oct.Z
PubAccessLists.Zumors.5Nov.Z
bin/
src/
```

3. That's all there to it. You've created your first UNIX directory, and you can now list it to see what it looks like:

```
% Is -ld NEWDIR
drwx------x 2 author 24 Nov 5 10:48 NEWDIR/
% Is -la NEWDIR
total 2
drwx------x 2 author 24 Nov 5 10:48 -/
drwx------ 1024 Nov 5 10:48 ../
```

Not surprisingly, the directory is empty other than the two defaults of " (the directory itself) and ".." (the parent directory, your home directory).

4. Look closely at the permissions of the directory. Remember that the permissions are a result of your umask setting. As you learned in the previous chapter, changing the umask setting changes the default permissions. Then, when you create a new directory, the new permissions will be in:

```
% umask 07
% umask 0
% mkdir NEWDIR
% Is -ld NEWDIR
drwx------x 2 author 24 Nov 5 10:53 NEWDIR2/
% umask 222
% mkdir NEWDIR
% Is -ld NEWDIR
dr-xr-xr-x 2 author 24 Nov 5 10:54 NEWDIR3/
```

5. What happens if you try to create a directory with a name that has already been used?

```
% mkdir NEWDIR
mkdir NEWDIR: File exists
```

6. To create a directory other than your current location, prefix the new directory name with a location:

```
% mkdir /tmp/test
% Is -l /tmp
-rwx------ 1 zhongqi 22724 4 Nov 5 21:33 /tmp/a.out*
-rw------ 1 julia 95594 4 Nov 5 23:10 /tmp/active.10122
-dr-xr-r-- 1 beast 572 Nov 5 05:59 /tmp/anon1
```

![](bbox=[0.858, 0.668, 0.982, 0.768])