# Chapter 10: Avoiding Shell Shock

The last line, :wq, writes the file to the disk and quits the editor.

Now you must tell Linux that it's okay to execute the file. To do this, you have to change the file permissions to execute:

```
chmod ugo+x, ugo+r
```

For more permissions, check out Chapter 8.

When you created the file, it was probably created with the permissions of the owner (u), the group (g), and the rest of the world (o) as at least being read (r), if not read and write (rw). The shell file, or shell script, should be able to be read (r) and executed (x) by the owner (that's), the people in the group, and the rest of the world.

Just because a shell can be read does not mean that it can be executed. You must explicitly tell the system that it's okay to execute it.

Now, type the following:

```
/quagmire
```

and you see your report run before your eyes!

```
/quagmire | more
```

and you see that your quagmire program acts like any other. It allows piping to other programs, including the printer (if you have one available to your system):

```
/quagmire | 1pr
```

But notice that for your program, you have to type . / in front of the filename. If you don't include . /, you get the following message:

```
bash: quagmire: command not found
```

This is because your current directory, where the quagmire shell script resides, is not in the list of directories contained in the PATH variable. If you type the following:

```
echo $PATH
```

you probably see a line that looks something like this:

```
/usr/local/bin:/bin:/usr/usr/X11R6/bin:/usr/bin/mh:/home/maddog/bin
```

![](bbox=[0.035, 0.363, 0.105, 0.433])