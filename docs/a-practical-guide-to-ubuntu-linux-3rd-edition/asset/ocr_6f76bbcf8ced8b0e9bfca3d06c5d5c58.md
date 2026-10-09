# tar: the `-x` option may extract a lot of files

**caution** Some tar archives contain many files. To list the files in the archive without unpacking them, run tar with the `-l` option and the name of the tar file. In some cases you may want to create a new directory (`mkdir` [page 208]), move the tar file into that directory, and expand it there. That way the unpacked files will not mingle with existing files, and no confusion will occur. This strategy also makes it easier to delete the extracted files. Depending on how they were created, some tar files automatically create a new directory and put the files into it; the `-t` option indicates where tar will place the files you extract.

# tar: the `-x` option can overwrite files

**caution** The `-x` option to tar overwrites a file that has the same filename as a file you are extracting. Follow the suggestion in the preceding caution box to avoid overwriting files.

**optional** You can combine the `gunzip` and `tar` commands on one command line with a pipe (`|`), which redirects the output of `gunzip` so that it becomes the input to `tar`:

```
```
$ gunzip -c make-3.81.tar.gz | tar -xvf -
```
```

The `-c` option causes `gunzip` to send its output through the pipe instead of creating a file. The final hyphen (`-`) causes `tar` to read from standard input. Refer to "Pipes" (page 251) and `gzip` (page 175) for more information about how this command line works.

A simpler solution is to use the `-z` option to `tar`. This option causes `tar` to call `gunzip` (or `gzip` when you are creating an archive) directly and simplifies the preceding command line to

```
```
$ tar -xvzf make-3.81.tar.gz
```
```

In a similar manner, the `-j` option calls `bzip2` or `bunzip2`.

# LOCATING COMMANDS

The `whereis` and `mlocate` utilities can help you find a command whose name you have forgotten or whose location you do not know. When multiple copies of a utility or program are present, which tells you which copy you will run. The `mlocate` utility searches for files on the local system.

# which AND whereis: LOCATE A UTILITY

When you give Linux a command, the shell searches a list of directories for a program with that name and runs the first one it finds. This list of directories is called a *search path*. For information on how to change the search path, refer to "PATH: Where the Shell Looks for Programs" on page 319. If you do not change the search path, the shell searches only a standard set of directories and then stops searching. However, other directories on the system may also contain useful utilities.

**which** The `which` utility locates utilities by displaying the full pathname of the file for the utility. (Chapter 6 contains more information on pathnames and the structure of the