![](bbox=[0.32, 0.09, 0.78, 0.35])

**Figure 6–7** Using `mv` to move names and temp

If the working directory is /home/max, Max can use the following command to move the files names and temp from the working directory to the literature directory:

```
$ mv names temp literature
```

This command changes the absolute pathnames of the names and temp files from /home/max/names and /home/max/temp to /home/max/literature/names and /home/max/literature/temp, respectively (Figure 6–7). Like most Linux commands, mv accepts either absolute or relative pathnames.

As you work with Linux and create more files, you will need to create new directories using mkdir to keep the files organized. The mv utility is a useful tool for moving files from one directory to another as you extend your directory hierarchy.

The cp utility works in the same way mv does, except that it makes copies of the existing-file-list in the specified directory.

# ### mv: MOVES A DIRECTORY

Just as it moves ordinary files from one directory to another, so mv can move directories. The syntax is similar except you specify one or more directories, not ordinary files, to move:

```
mv existing-directory-list new-directory
```

If new-directory does not exist, the existing-directory-list must contain just one directory name, which mv changes to new-directory (mv renames the directory). Although you can rename directories using mv, you cannot copy their contents with cp unless you use the -r (recursive) option. Refer to the tar and cpio man pages for other ways to copy and move directories.