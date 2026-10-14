# Table 4-9: rm Examples

| Command | Results |
|---|---|
| rm file1 | Delete file1 silently. |
| rm -i file1 | Before deleting file1, prompt the user for confirmation. |
| rm -r file1 dir1 | Delete file1 and dir1 and its contents. |
| rm -rf file1 dir1 | Same as above, except that if either file1 or dir1 does not exist, rm will continue silently. |

# In—Create Links

The ln command is used to create either hard or symbolic links. It is used in one of two ways:

```
ln file link
```

to create a hard link and

```
ln -s item link
```

to create a symbolic link where item is either a file or a directory.

# Hard Links

Hard links are the original Unix way of creating links; symbolic links are more modern. By default, every file has a single hard link that gives the file its name. When we create a hard link, we create an additional directory entry for a file. Hard links have two important limitations:

+   - A hard link cannot reference a file outside its own filesystem. This means a link cannot reference a file that is not on the same disk partition as the link itself.
+   - A hard link cannot reference a directory.

A hard link is indistinguishable from the file itself. Unlike a directory list containing a symbolic link, a directory list containing a hard link shows no special indication of the link. When a hard link is deleted, the link is removed, but the contents of the file itself continue to exist (that is, its space is not deallocated) until all links to the file are deleted.

It is important to be aware of hard links because you might encounter them from time to time, but modern practice prefers symbolic links, which we will cover next.

# Symbolic Links

Symbolic links were created to overcome the limitations of hard links. Symbolic links work by creating a special type of file that contains a text pointer