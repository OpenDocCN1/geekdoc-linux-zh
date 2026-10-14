# 4 – Manipulating Files And Directories

Let's pass the fun around a little by moving our renamed file to each of the directories and back again:

```
`[me@linuxbox playground]$ mv fun dir1`
```

to move it first to directory `dir1`, then:

```
`[me@linuxbox playground]$ mv dir1/fun dir2`
```

to move it from `dir1` to `dir2`, then:

```
`[me@linuxbox playground]$ mv dir2/fun .`
```

to finally bring it back to the current working directory. Next, let's see the effect of `mv` on directories. First we will move our data file into `dir1` again:

```
`[me@linuxbox playground]$ mv fun dir1`
```

then move `dir1` into `dir2` and confirm it with `ls`:

```
```text
[me@linuxbox playground]$ mv dir1 dir2
[me@linuxbox playground]$ ls -l dir2
total 4
drwxrwxr-x 2 me me 4096 2008-01-11 06:06 dir1
[me@linuxbox playground]$ ls -l dir2/dir1
total 4
-rw-r--r-- 1 me me 1650 2008-01-10 16:33 fun
```
```

Note that since `dir2` already existed, `mv` moved `dir1` into `dir2`. If `dir2` had not existed, `mv` would have renamed `dir1` to `dir2`. Lastly, let's put everything back:

```
```text
[me@linuxbox playground]$ mv dir2/dir1 .
[me@linuxbox playground]$ mv dir1/fun .
```
```