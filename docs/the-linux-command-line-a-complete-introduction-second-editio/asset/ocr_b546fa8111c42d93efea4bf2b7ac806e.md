```
[me@linuxbox playground]$ mv dir1/fun dir2
```

Finally, this command brings it back to the current working directory:

```
[me@linuxbox playground]$ mv dir2/fun .
```

Next, let’s see the effect of mv on directories. First we will move our data file into dir1 again, like this:

```
[me@linuxbox playground]$ mv fun dir1
```

Then we move dir1 into dir2 and confirm it with ls.

```
[me@linuxbox playground]$ mv dir1 dir2
[me@linuxbox playground]$ ls -l dir2
total 4
drwxrwxr-x 2 me me 4096 2018-01-11 06:06 dir1
[me@linuxbox playground]$ ls -l dir2/dir1
total 4
-rw-r--r-- 1 me me 1650 2018-01-10 16:33 fun
```

Note that because dir2 already existed, mv moved dir1 into dir2. If dir2 had not existed, mv would have renamed dir1 to dir2. Lastly, let’s put everything back.

```
[me@linuxbox playground]$ mv dir2/dir1 .
[me@linuxbox playground]$ mv dir1/fun .
```

# Creating Hard Links

Now we’ll try some links. We’ll first create some hard links to our data file, like so:

```
[me@linuxbox playground]$ ln fun fun-hard
[me@linuxbox playground]$ ln fun dir1/fun-hard
[me@linuxbox playground]$ ln fun dir2/fun-hard
```

So now we have four instances of the file fun. Let’s take a look at our playground directory.