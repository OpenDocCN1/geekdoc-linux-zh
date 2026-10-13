the same **group** as the file’s owner (the next three characters), and finally all other users on the system (the last three characters). Generally, they indicate whether the specified class of user can read the file, write to the file, or execute the contents of the file (in the case of a program or shell script).

The `ls -l` command then shows the link count (see “Linking Files: The ln Command,” later in this chapter), the owner of the file, the group owner of the file, how large the file is (that is, how many characters are contained in it), and when the file was last modified. The information displayed last on the line is the filename itself.

> > **Note**
> >
> > Many modern Unix systems have gone away from using groups, so while those permissions are still shown, the group owner for a specific file or directory is often omitted in the output of the `ls` command.

You should now be able to glean a lot of information from the `ls -l` output for a directory full of files:

```
```shell
$ ls -l programs
total 4

-rwxr-xr-x  1 steve  DP3725   358 Jun 25 13:31 collect
-rwxr-xr-x  1 steve  DP3725  1219 Jun 25 13:31 mon
-rwxr-xr-x  1 steve  DP3725    89 Jun 25 13:30 wb
$
```
```

The dash in the first column of each line indicates that the three files collect, mon, and wb are ordinary files and not directories. Now, can you figure out how big are they?

# Creating a Directory: The mkdir Command

Use `mkdir` to create directories. The argument to this command is simply the name of the directory you want to create. For example, assume that you are still working with the directory structure depicted in Figure 1.7 and that you want to create a new directory called `misc` at the same level as the directories documents and programs. If you were currently in your home directory, typing the command `mkdir misc` would achieve the desired effect:

```
```shell
$ mkdir misc
$
```
```

Now if you run `ls`, you will have the new directory listed:

```
```shell
$ ls
documents
misc
programs
$
```
```