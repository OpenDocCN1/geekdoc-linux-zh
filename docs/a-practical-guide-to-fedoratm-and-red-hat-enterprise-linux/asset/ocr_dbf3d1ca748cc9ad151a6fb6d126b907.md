# ARGUMENTS

The first form of *mv* takes two arguments: the pathname of the ordinary file you want to rename and/or move and the new pathname of the file. The first of the following commands renames **memo** in the working directory to **memo.copy**. The second command moves **memo** from the working directory to the **copies** directory and renames it **memo.130808**.

```
$ mv memo memo.copy
$ mv memo copies/memo.130808
```

The second form of *mv* takes two or more arguments; all but the last are the pathnames of ordinary files you want to move and the last specifies the new parent directory for the files. The files you move will have the same simple filenames as each of the original files but new absolute pathnames. The following command moves **memo1**, **memo2**, and **memo3** from the working directory and **memoX** from the */tmp* directory to the (existing) **memo.copy** subdirectory of the working directory.

```
$ mv memo1 memo2 memo3 /tmp/memoX memo.copy
```

The third form of *mv* takes two arguments: the pathname of an existing directory that you want to move and/or rename, and the new pathname for the directory, which does not exist. (If the directory exists, the command is the second form of *mv* and moves the file to the directory without changing the file’s name.) The first of the following commands renames the **memo.copy** directory in the working directory **memo.old**. The second moves the **feb** subdirectory of **memos** to the directory named **archive** and renames it **1302**.

```
$ mv memo.copy memo.old
$ mv memos/feb archive/1302
```

# OPTIONS

The *-f* (--force) option causes *mv* **not** to prompt you if a move would overwrite an existing file that you do not have write permission for. You must have write permission for the directory holding the existing file.

The *-i* (--interactive) option prompts for confirmation if *mv* would overwrite a file. If your response begins with a **y** or **Y**, *mv* overwrites the file; otherwise, *mv* does not move the file. The following example copies all files named **memoX** followed by a single character to the **memo.copy** directory, prompting you if it would overwrite a file.

```
$ mv -i memo? memo.copy
mv: overwrite 'memo.copy/memo3'? y
```

If *mv* would not overwrite a file, it does not prompt even with this option.

The *-v* (--verbose) option lists files as they are moved.

```
$ mv -v memo? memo.copy
'memo1' -> 'memo.copy/memo1'
'memo2' -> 'memo.copy/memo2'
```