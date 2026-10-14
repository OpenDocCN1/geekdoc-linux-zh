# 5.1.3 Making a Directory Tree

Use mkdir with the -p option to make a subdirectory and any of its parents that do not already exist. This is useful when you want to make a fairly complex directory tree from scratch and don’t want to have to make each directory individually.

⇒ To make the work/completed/2001 directory—a subdirectory of the completed directory, which in turn is a subdirectory of the work directory in the current directory, type:

```
$ mkdir -p work/completed/2001 [RET]
```

This makes a 2001 subdirectory in the directory called completed, which in turn is in a directory called work in the current directory; if the completed or the work directories do not already exist, they are made as well. If you know that work and completed both exist, the previous command works fine without the -p option.

# 5.1.4 Using a File with Spaces in Its Name

While a space character is not forbidden in naming files, it does make them difficult to use. Sometimes you might get one made on a system running MacOS, where space characters are common in file names. If a directory or file has a space in its name, there are two methods for specifying the name on the command line.

To reference a file with a space character in its name, quote the name (see Recipe 3.1.3 [Quoting Reserved Characters], page 56). The following methods are variations on this.

# METHOD #1

To use a file with space in its name, enclose the file in single-quote characters (').

⇒ To list the contents of the directory named Top Secret, type:

```
$ ls 'Top Secret' [RET]
```

You can also use double quote characters (") to quote; if a file name contains one kind of quote in its name, use the other.

⇒ To list the contents of the directory named McHale's Restaurant, type:

```
$ ls "McHale's Restaurant" [RET]
```