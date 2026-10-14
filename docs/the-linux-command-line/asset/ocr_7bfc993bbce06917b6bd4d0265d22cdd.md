```
[me@linuxbox playground]$ rm -i fun
rm: remove regular file `fun'?
```

Enter “y” at the prompt and the file is deleted. But let’s look at the output of ls now. Noticed what happened to fun-sym? Since it’s a symbolic link pointing to a now-nonexistent file, the link is broken:

```
[me@linuxbox playground]$ ls -l
total 8
drwxrwxr-x 2 me me 4096 2008-01-15 15:17 dir1
lrwxrwxrwx 1 me me 4 2008-01-16 14:45 dir1-sym -> dir1
drwxrwxr-x 2 me me 4096 2008-01-15 15:17 dir2
lrwxrwxrwx 1 me me 3 2008-01-15 15:15 fun-sym -> fun
```

Most Linux distributions configure ls to display broken links. On a Fedora box, broken links are displayed in blinking red text! The presence of a broken link is not, in and of itself dangerous but it is rather messy. If we try to use a broken link we will see this:

```
[me@linuxbox playground]$ less fun-sym
fun-sym: No such file or directory
```

Let’s clean up a little. We’ll delete the symbolic links:

```
[me@linuxbox playground]$ rm fun-sym dir1-sym
[me@linuxbox playground]$ ls -l
total 8
drwxrwxr-x 2 me me 4096 2008-01-15 15:17 dir1
drwxrwxr-x 2 me me 4096 2008-01-15 15:17 dir2
```

One thing to remember about symbolic links is that most file operations are carried out on the link’s target, not the link itself. rm is an exception. When you delete a link, it is the link that is deleted, not the target.

Finally, we will remove our playground. To do this, we will return to our home directory and use rm with the recursive option (-r) to delete playground and all of its contents, including its subdirectories:

```
[me@linuxbox playground]$ cd
```