```
    -rw-r--r-- 1 user2    ourfiles  747  April 12 11:35 myfile
    lrwxrwxrwx 1 user2  ourfiles   7 April 12 11:38 /tmpfile/s2 ->
      myfiie
```

As you will note, file sizes and modification dates are different for these two files. The status information is also different. The l in the line of output indicates a link.

You can use this same type of command to create a symbolic link to a directory. If you use the -s option, the system interprets it for either a file or a directory. You can change directories if you use a symbolic link as an argument to the cd utility. Be careful, however, because it is easy to get confused, especially if you do not realize you are using a symbolic link. The security of your files depends upon carefully thought-out linking because links provide access to files that you might not realize exist if you don't pay attention.

When you are in either the Bourne shell or the C shell, you can use cd to change directories to find a symbolic link to a directory. The pwd (parent working directory) command displays the name of the original directory and not the linked directory. If you use cd to change your working directory to the parent directory, you will be in the parent of the original directory, not the parent of the linked directory. This can create confusion if you do not understand how it works.

# Korn Shell Linked Directories

The Korn shell handles symbolically linked directories differently than the Bourne and C shells handle them. It will keep track of the symbolic links when using cd to move into a linked directory and when moving back to the parent of that directory. You can tell where you really are by using /usr/bin/pwd. The pwd built-in on ksh will show you where you are according to the symbolic link:

```
$ mkdir foo; ln -s foo bar
$ ls -la foo bar
drwxr-xr-x     2 guest staff      512 Jun  6 00:03 foobar
lrwxrwxrwx     1 guest staff        6 Jun  6 00:03 nit -> foobar
$ cd bar
$ pwd

/usr/people/guest/nit

$ /usr/bin/pwd

/usr/people/guest/foobar
$
```