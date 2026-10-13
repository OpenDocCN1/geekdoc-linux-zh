This command basically says to subtract read permissions (indicated by the r) from the group and from other (indicated by the g and the o). If we now do a directory listing, the entry for file1 will look like this:

```
-rw...... 1 murban murban 0 Oct 29 06:28 file1
```

What if we want to give read permissions back to the group? As you might have guessed, the command to do this would be:

```
chmod g+r file1
```

There are some other ways that you can set file permissions using the chmod command, but they are beyond the scope of this book. Please see the man page for chmod if you are interested. Man pages were discussed earlier in this hour. Also, see Hour 5 for more information on users and groups.

![](bbox=[0.22, 0.6, 0.3, 0.72])

> There are a couple of potential pitfalls you need to be aware of with file permissions. The main thing you need to keep in mind is that directory permissions can override file permissions. This means, for example, that if the group has write access to a directory, anyone in that group will be able to delete any file in that directory, even if they do not have write access to the file itself. (The write privileges on the directory allow them to make changes to the directory.) Another thing to note is that if someone has execute privileges on a directory, but does not have read privileges on it, they will be able to go into the directory, but they will not be able to list the contents of the directory. However, they will still be able to read files in that directory provided that they know the name of the file.

# Process Management

As we have mentioned in previous hours, FreeBSD is a multitasking operating system. This means that you can have several processes running at the same time. Many of them might be running in the background. You can use the ps command to see a list of processes that you are currently running. If you run ps with no options, it will give you a list of only the processes that are owned by you. Several useful options to ps can be used to change what it shows you. Table 4.2 shows some of the most common and useful ones.