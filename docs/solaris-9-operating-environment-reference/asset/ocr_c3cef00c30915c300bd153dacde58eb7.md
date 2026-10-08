# In

# 699

# Notes

A symbolic link to a directory behaves differently than you might expect in certain cases. While an ls(1) on such a link displays the files in the pointed-to-directory, an ls -l displays information about the link itself, as shown in the following example.

```
castle$ ln -s dir link
castle$ ls link
file1 file2 file3
castle$ ls -l link
lrwxr-wx 1 user      Jan 11 23:27 link -> dir
castle$
```

When you use cd(1) to change a directory through a symbolic link, you wind up in the pointed-to location within the file system. This means that the parent of the new working directory is not the parent of the symbolic link, but rather, the parent of the pointed-directory. For instance, in the following case, the final working directory is /usr and not /home/user/linktest.

```
castle$ pwd
/home/user/linktest
castle$ ln -s /usr/tmp symlink
castle$ cd symlink
castle$ ..
castle$ pwd
/usr
castle$
```

C shell users can avoid any resulting navigation problems by using pushd and pop built-in commands instead of cd.

# Options

The following options are supported for both /usr/bin/ln and /usr/xpg4/bin/ln.

+   -f Link files without questioning or if the mode of target forbids writing (the default if standard input is not a terminal).
-s Create a symbolic link.

If you use the -s option with two arguments, target can be an existing directory or a nonexistent file. If target already exists and is not a directory, an error is returned. source-file can be any name and not not exist. If it exists, it can be a file or directory and can reside on a different file system from target. If target is an existing directory, a file is created in directory target whose name is source-file or the last component of source-file is a symbolic link that references source-file. If target does not exist, a file with name target is created and a symbolic link that references source-file.

If you use the -s option with more than two arguments, target must be an existing directory or an error is returned. For each source-file, a link is created in target whose name is the last component of source-file, each new source-file is a symbolic link to the original source-file. The files and target can reside on different file systems.