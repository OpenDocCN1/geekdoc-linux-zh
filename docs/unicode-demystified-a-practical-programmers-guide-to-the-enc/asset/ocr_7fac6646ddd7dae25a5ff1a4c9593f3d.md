When you use a wildcard character (such as *) in a remote pathname, you must quote the wildcard character so that it is interpreted by the shell on the remote machine and not by the local shell.
As with cp, if the destination-file exists before you run scp, scp overwrites the file.

# Examples

The first example copies the files with filenames ending in .c from the working directory on the local machine into the ~jenny/archives directory on bravo. The wildcard character is not quoted, because it is to be expanded by the local shell. Because archives is a relative pathname, scp assumes that it is a subdirectory of jenny's home directory on bravo. Each of the copied files retains its filename:

```
$ scp *.c jenny@bravo:archives
```

Next, Alex copies the directory structure under ~alex/memos on bravo to ~jenny/alex.memos.bravo on kudos. Alex must have the necessary permissions to write to jenny's home directory on kudos:

```
$ scp -r bravo:memos jenny@kudos:alex.memos.bravo
```

Finally, Alex copies the files with filenames ending in .c from jenny's archives on bravo to the jenny.c.bravo directory in his working directory. The wildcard character is quoted because it is to be interpreted by the remote machine, bravo:

```
$ scp -r 'jenny@bravo:archives/*.c' jenny.c.bravo
```

It is important to remember that whenever you copy multiple files or directories, the destination—either local or remote—must be an existing directory and not an ordinary or nonexistent file.