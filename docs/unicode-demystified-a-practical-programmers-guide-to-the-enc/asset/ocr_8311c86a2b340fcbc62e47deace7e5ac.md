# cd

Changes to another working directory
cd (directory)

Without an argument cd makes your home directory the working directory. With a directory path-
name as an argument, cd makes that directory the working directory.

# Argument

The directory is the pathname of the directory you want to become your new working
directory.

# Notes

The cd program is a builtin in bash, tsh, and zsh. Refer to the discussions of the
HOME shell variable on pages 576 and 708. Chapter 4 contains a discussion of cd
on page 108.

Each of the three shells has a variable (CDPATH or cdpath) that affects
t operation of cd. The CDPATH variable contains a list of directories cd searches
in addition to the working directory. If CDPATH is not set, cd searches only the
working directory. If CDPATH is set, cd searches each of the directories in CD-
PATH's directory list. Refer to page 580 for more information about CDPATH or
to page 707 for more information about cdpath.

The Z Shell builtin has features in addition to those common to all three
shells.

# Examples

The following command makes your home directory become the working directory:

```
$ cd
```

The next command makes the /home/alex/literature directory the working di-
rect. The next pwd verifies the change:

```
$ cd /home/alex/literature
$ pwd
/home/alex/literature
```

Next, the cd utility makes a subdirectory of the working directory the new
working directory: