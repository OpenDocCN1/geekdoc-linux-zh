Let's take a look at the files in the current working directory:

```
$ ls
documents
programs
$
```

If you supply the name of one of these directories to the `ls` command, you can get a list of the contents of that directory. So you can find out what's contained in the documents directory by typing the command `ls documents`:

```
$ls documents
letters
memos
proposals
$
```

To take a look at a subdirectory memos, you can follow a similar procedure:

```
$ls documents/memos
dact
plan
$
```

If you specify a nondirectory file argument to the `ls` command, you simply get that filename echoed back at the terminal:

```
$ls documents/memos/plan
documents/memos/plan
$
```

Confused? There's an option to the `ls` command that lets you determine whether a particular file is a directory, among other things. The `-l` option (the letter l) provides a more detailed description of the files in a directory. If you were currently in steve's home directory, here's what the `-l` option to the `ls` command produces: 

```
$ls -l
total 2
drwxr-xr-x 5 steve DP3725 80 Jun 25 13:27 documents
drwxr-xr-x 2 steve DP3725 96 Jun 25 13:31 programs
$
```

The first line of the display is the count of blocks (1,024 bytes) of storage that the listed files use. Each successive line displayed by the `ls -l` command contains information about a file in the directory. The first character on each line indicates what type of file it is: `d` for a directory, `-` for a file, `b`, `c`, `l`, or `p` for a special file.

The next characters on the line define the permissions of that particular file or directory. These access modes apply to the file's owner (the first three characters), other users in