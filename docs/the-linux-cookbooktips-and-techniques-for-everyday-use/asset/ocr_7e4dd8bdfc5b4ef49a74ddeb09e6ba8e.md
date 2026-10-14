# The Linux Cookbook: Tips and Techniques for Everyday Use:

+   • To move the file `/usr/tmp/notes` to the current working directory, type:

```
$ mv /usr/tmp/notes . RET
```

This command moves the file `/usr/tmp/notes` to the current working directory.

To move a directory, give the path name of the directory you want to move and the path name to move it to as arguments.

+   • To move the directory `work` in the current working directory to `play`, type:

```
$ mv work play RET
```

This command moves the directory `work` in the current directory to the directory `play`. If the directory `play` already exists, mv puts `work` inside `play`---it does not overwrite directories.

Renaming a file is the same as moving it; just specify as arguments the file to rename followed by the new file name.

+   • To rename the file `notes` to `notes.old`, type:

```
$ mv notes notes.old RET
```

6.5.1 Changing File Names to Lowercase

6.5.2 Renaming Multiple Files with the Same Extension

Changing the case of a file.

Renaming multiple files at once.

# 6.5.1 Changing File Names to Lowercase

@sf (WWW): http://eternity.2y.net/chcase

To change the uppercase letters in a file name to lowercase (or vice versa), use chcase. It takes as arguments the files whose names it should change.

+   • To change the file names of all of the files in the current directory to lowercase letters, type:

```
$ chcase * RET
```