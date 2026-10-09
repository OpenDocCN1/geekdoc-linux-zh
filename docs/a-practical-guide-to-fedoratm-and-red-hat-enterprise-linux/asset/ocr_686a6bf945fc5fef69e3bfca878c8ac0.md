![](bbox=[0.07, 0.11, 0.12, 0.13])

# ls: Displays Information About Files

The `ls` utility displays information about one or more files. It lists the information alphabetically by filename unless you use an option to change the order.

When you do not provide an argument, `ls` displays the names of the visible files (those with filenames that do not begin with a period; page 180) in the working directory.

# ARGUMENTS

The arguments are one or more pathnames of any ordinary, directory, or device files. The shell expands ambiguous file references (page 165) in the arguments.

When you specify an ordinary file as an argument, `ls` displays information about that one file. When the argument is a directory, `ls` displays the contents of the directory. It displays the name of the directory only when needed to avoid ambiguity, such as when the listing includes more than one directory.

```
```
$ ls memos.zach/130715.1
memos.zach/130715.1

$ ls memos.zach
130712.1  130714.2  130714.3  130715.1

$ ls memos.*
memos.max:
130619.1  130621.2  130622.1

memos.sam:
130811.2  130811.3  130812.1

memos.zach:
130712.1  130714.2  130714.3  130715.1
```
```

![](bbox=[0.21, 0.62, 0.26, 0.64])

# OPTIONS

Options determine the type of information `ls` displays, and the manner and order in which it displays the information. When you do not use an option, `ls` displays a short list that contains just the names of files, in alphabetical order. See page 145 for examples of how options affect `ls` output.

All  -a (--all) option includes hidden filenames (those filenames that begin with a period; page 180) in the listing. Without this option `ls` does not list information about files with hidden filenames unless you specify the name of a hidden file as an argument. The `*` ambiguous file reference does not match a leading period in a filename, so you must use this option or explicitly specify a filename (ambiguous or not) that begins with a period to display information about files with hidden filenames.

![](bbox=[0.21, 0.83, 0.25, 0.85])

Directory

The `-d` (--directory) option displays directories without displaying their contents.

```
```
$ ls -ld /
dr-xr-xr-x  27 root root  4096 07-16 18:37 /
```
```

This option is useful when you want to find out, for example, the name of the user who owns a directory in a large directory such as /etc. Instead of scrolling through