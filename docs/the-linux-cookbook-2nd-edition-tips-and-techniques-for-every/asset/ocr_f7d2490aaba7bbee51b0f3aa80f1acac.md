contents of a directory recursively, outputting a listing of that directory and the contents of all of its subdirectories.

⇒ To output a recursive directory listing of the current directory, type:

```
$ ls -R [RET]
play    work

play:
notes

work:
notes
$
```

In this example, the current working directory contains two subdirectories, work and play, and no other files. Each subdirectory contains a file called notes.

⇒ To list all of the files on the system, type:

```
$ ls -R / [RET]
```

This command recursively lists the contents of the root directory, /, and all of its subdirectories. It is common to combine this with the attribute option, -l, to output a verbose listing of all the files on the system:

```
$ ls -lR / [RET]
```

NOTES: You can’t list the contents of some directories on the system if you don’t have permission to do so (see Recipe 6.3 [Controlling Access to Files], page 167).

# 5.4 Copying Files and Directories

Use cp (“copy”) to copy files. It takes two arguments: the source file, which is the existing file to copy, and the target file, which is the file name for the new copy. The cp command then makes an identical copy of the source file, giving it the specified target name. If a file with the target name already exists, cp overwrites it. It does not alter the source file.

⇒ To copy the file my-copy to the file neighbor-copy, type:

```
$ cp my-copy neighbor-copy [RET]
```