# # Hard links

A *hard link* maintains the same permissions and access times of the original file; in fact, both have the same inode number. The hard link simply appears to have a different filename and/or location. Changes to either the original file or the link affect both. The two files have equal importance. However, deleting either of the files won't affect the other. The hard link files appear to be regular files when examined and they function this way as well.

Hard links do have certain limitations, however: Normal users can't create hard links to directories. Also, hard links aren't allowed to span file systems.

To create a hard link, you use the `ln` command. An example of creating a hard link of the *stuff* file to */home/angie/stuff* is as follows:

```
```
# ln stuff2 /home/angie/stuff
# ls -al
-rw-r--r--   2 root     root      89704 Aug 27  2000 stuff
-rw-r--r--   2 root     root      89704 Aug 27  2000 stuff2
```
```

As you can see from the above example these files are the same size. The number two that appears after the permissions indicates that two hard links of the file exist.

# # Symbolic links

The other type of link is a *symbolic or soft link*. These links allow a greater degree of flexibility. Users can create symbolic links to directories, and symbolic links can span file systems. Links can even be created to nonexistent files. The symbolic link maintains permissions separate from those of the original file. Deleting the original file won't remove the symbolic link, but the file itself will be removed. This can cause the symbolic link to no longer function.

To create a soft link, you use the `ln` command as displayed in the following example. Here a soft link of the *stuff* file is created at */home/angie/stuff*.

```
```
# ln -s stuff /home/angie/stuff
```
```

Soft links can be identified by listing the details of a directory's contents. This is shown in the following example.

```
```
# ls -al
lrwxrwxrwx   1 angie      angie        7 Mar 10 17:06 stuff -> /fun/stuff
```
```

It is important to understand that although opening, reading, and writing to a link affects the target file, removing the symbolic link removes only the link, not the target. When the symbolic link file is copied, the original file is placed in the target location. This is an independent copy of the original file and changes to this copy do not affect the original.