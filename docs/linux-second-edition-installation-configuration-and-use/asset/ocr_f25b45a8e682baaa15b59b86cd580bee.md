# COMMAND REFERENCE

alias abbreviation in /etc/profile. The most important special characters are: for directories, @ for symbolic links, * for executable files and for FIFOs (see page 393).

-r or --reverse
verses the sorting order. This option is frequently used in combination with -n -t or -S.

-R or --recursive
also displays files in subdirectories (like /S with the DOS command DIR).

-s or --sort=size
sorts the files by size (the largest file first).

-t or --sort=time
sorts the files by time and date of last modification (the most recent file).

-u or --sort=access
sorts the files by time and date of the last access. This option must be specified with -t (otherwise, ls does not sort at all).

-X or --sort=extension
sorts the files by their extension (the character combination after the last . in the file name).

The output of ls with the -l option needs some explanation. A typical line looks like this:

```
-rw-r---- 1 michael users 3529 Oct 4 15:43 header.tex
```

Thus, we are talking about the file header.tex, which was last modified at 15:43 on 4 October of the current year. The file is 3529 bytes long and belongs to somebody from the group whose name is michael. The ten characters at the beginning of the line specify file type and access rights. File type indicators like the hyphen - for a normal file, d for a directory, b or c for a file (block char) and l for a symbolic link. The next three characters (rwx) specify whether the user is allowed to read, write or execute the file. Analogous information follows for the members of the group and for all other users.

In contrast to the DOS command DIR, ls does not show the entire space taken by listed files. This is the task of du (see page 451).

In respect, ls differs substantially from the DOS command while: DIR /S *.abc lists files in subdirectories, the seemingly analogous command ls -R *.abc fails. The reason is that the file name expansions for *.abc are not executed by the command itself, but by the command interpreter (bash, she) and only to the current directory. If you want to find files in arbitrary directories, you must use find (see page 454).

# Examples

```
user$ ls -ltr /root
displays all files in the /root directory and sorts them by date (the most recent last).
```