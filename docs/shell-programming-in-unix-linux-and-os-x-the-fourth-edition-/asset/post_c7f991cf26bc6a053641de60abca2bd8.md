
Look closely at the second column of the output: The number shown is 1 for collect and mon and 2 for wb and writeback. This is the number of links to a file, normally for nonlinked, nondirectory files. Because wb and writeback are linked, however, this number is 2 for these files (or, more correctly, this file with two names).

You can remove either of the two linked files at any time, and the other will not be removed:

```text
$ rm writeback
$ ls -l
total 4
-rwxr-xr-x  1 steve    DP3725      358 Jun 25 13:31 collect
-rwxr-xr-x  1 steve    DP3725     1219 Jun 25 13:31 mon
-rwxr-xr-x  1 steve    DP3725       89 Jun 25 13:30 wb
$
```

Note that the number of links on wb went from 2 to 1 because one of its links was removed.

Most often, ln is used to allow a file to appear in more than one directory simultaneously. For example, suppose that pat wanted to have access to steve’s wb program. Instead of making a copy for himself (subject to the same data sync problems described previously) or including steve’s programs directory in his PATH (which has security risks as described in Chapter 10, “Your Environment”), he can simply link to the file from his own program directory:

```text
$ pwd
/users/pat/bin                         pat’s program directory
$ ls -l
total 4
-rwxr-xr-x  1 pat      DP3822     1358 Jan 15 11:01 lcat
-rwxr-xr-x  1 pat      DP3822      504 Apr 21 18:30 xtr
$ ln /users/steve/wb .                link wb to pat’s bin
$ ls -l
total 5
-rwxr-xr-x  1 pat      DP3822     1358 Jan 15 11:01 lcat
-rwxr-xr-x  2 steve    DP3725       89 Jun 25 13:30 wb
-rwxr-xr-x  1 pat      DP3822      504 Apr 21 18:30 xtr
$
```

Note that steve is still listed as the owner of wb, even when viewing the contents of pat’s directory. This makes sense, because there’s really only one copy of the file and it’s owned by steve.

The only stipulation on linking files is that for ordinary links the files to be linked together must reside on the same file system. If they don’t, you’ll get an error from ln when you try to link them. (To determine the different file systems on your system, execute the df command. The first field on each line of output is the name of a file system.)

To create links on files on different file systems (or on different networked systems), you can use the -s option to the ln command. This creates a symbolic link. Symbolic links behave a lot like regular links, except that the symbolic link points to the original file; if the original file is removed, the symbolic link no longer works.

Let’s see how symbolic links work with the previous example:

```text
$ rm wb
$ ls -l
total 4
-rwxr-xr-x  1 pat     DP3822    1358 Jan 15 11:01 lcat
-rwxr-xr-x  1 pat     DP3822     504 Apr 21 18:30 xtr
$ ln -s /users/steve/wb ./symwb                 Symbolic link to wb
$ ls -l
total 5
-rwxr-xr-x  1 pat     DP3822    1358 Jan 15 11:01 lcat
lrwxrwxr-x  1 pat     DP3822      15 Jul 20 15:22 symwb -> /users/steve/wb
-rwxr-xr-x  1 pat     DP3822     504 Apr 21 18:30 xtr
$
```

Note that pat is listed as the owner of symwb, and the file type shown as the very first character in the ls output is l, which indicates a symbolic link. The size of the symbolic link is 15 (the file actually contains the string /users/steve/wb), but if we attempt to access the contents of the file, we are presented with the contents of the file it’s linked to, /users/steve/wb:

```text
$ wc symwb
       5           9          89 symwb

$
```

The -L option to the ls command can be used with the -l option to get a detailed list of information on the file the symbolic link points to:

```text
$ ls -Ll
total 5
-rwxr-xr-x  1 pat     DP3822    1358 Jan 15 11:01 lcat
-rwxr-xr-x  1 steve   DP3725      89 Jun 25 13:30 wb
-rwxr-xr-x  1 pat     DP3822     504 Apr 21 18:30 xtr
$
```

Removing the file that a symbolic link points to invalidates the symbolic link (because symbolic links are maintained as filenames), but it doesn’t remove it:

```text
$ rm /users/steve/wb                         Assume that pat can remove this file
$ ls -l
total 5
-rwxr-xr-x  1 pat     DP3822    1358 Jan 15 11:01 lcat
lrwxrwxr-x  1 pat     DP3822      15 Jul 20 15:22 symwb -> /users/steve/wb
-rwxr-xr-x  1 pat     DP3822     504 Apr 21 18:30 xtr
$ wc symwb
Cannot open wb: No such file or directory
$
```

This type of file is called a *dangling symbolic link* and should be removed unless you have a specific reason to keep it around (for example, if you intend to replace the removed file).

One last note before leaving this discussion: The `ln` command follows the same general format as `cp` and `mv`, meaning that you can create links to a bunch of files within a specific target directory using the format

```text
ln files directory
```

## Removing a Directory: The `rmdir` Command

You can remove a directory with the `rmdir` command. Rather than let you accidentally remove dozens or hundreds of files, however, `rmdir` won't let you proceed unless the specified directory is completely empty of files and subdirectories.

To remove the directory `/users/pat`, we could use the following:

```text
$ rmdir /users/pat
rmdir: pat: Directory not empty
$
```

Phew! That would have been a mistake! Instead, let's remove the `misc` directory that you created earlier:

```text
$ rmdir /users/steve/misc
$
```

Once again, the preceding command works only if no files or directories are contained in the `misc` directory; otherwise, the following happens, as also shown earlier:

```text
$ rmdir /users/steve/misc
rmdir: /users/steve/misc: Directory not empty
$
```

If you still want to remove the `misc` directory, you would first have to remove all the files contained in that directory before reissuing the `rmdir` command.

As an alternative method for removing a directory and its contents, you can use the `-r` option to the `rm` command. The format is simple:

```text
rm -r dir
```

where `dir` is the name of the directory that you want to remove. `rm` removes the indicated directory and all files (including directories) in it, so be careful with this powerhouse command.

Want to go full turbo? Add the `-f` flag and it forces the action without prompting you on a command-by-command basis. It can completely trash your system if you're not careful, however, so many admins simply avoid `rm -rf` entirely!

## Filename Substitution

### The Asterisk

One powerful feature of the Unix system that is handled by the shell is *filename substitution*. Let’s say that your current directory has these files in it:

```text
$ ls
chap1
chap2
chap3
chap4
$
```

Suppose that you want to display their contents en masse. Easy: `cat` allows you to display the contents of as many files as you specify on the command line. Like this:

```text
$ cat chap1 chap2 chap3 chap4
    ...
$
```

But that’s tedious. Instead, you can take advantage of filename substitution by simply typing:

```text
$ cat *
    ...
$
```

The shell automatically substitutes the names of all the files in the current directory that match the pattern *. The same substitution occurs if you use * with another command too, of course. How about echo?

```text
$ echo *
chap1 chap2 chap3 chap4
$
```

Here the * is again replaced with the names of all the files contained in the current directory, and the echo command simply displays that list to you.

Any place that * appears on the command line, the shell performs its substitution:

```text
$ echo * *
chap1 chap2 chap3 chap4 : chap1 chap2 chap3 chap4
$
```

The * is part of a rich file substitution language, actually, and it can also be used in combination with other characters to limit which filenames are matched.

For example, let’s say that in your current directory you have not only chap1 through chap4 but also files a, b, and c:

```text
$ ls
a
b
c
chap1
chap2
chap3
chap4
$
```

To display the contents of just the files beginning with chap, you can type in

```sh
$ cat chap*
    .
    .
    .
$
```

The chap* matches any filename that begins with chap. All such filenames matched are substituted on the command line before the specified command is even invoked.

The * is not limited to the end of a filename; it can be used at the beginning or in the middle as well:

```sh
$ echo *t1
chap1
$ echo *t*
chap1 chap2 chap3 chap4
$ echo *x
*x
$
```

In the first echo, the *t1 specifies all filenames that end in the characters t1. In the second echo, the first * matches everything up to a t and the second everything after; thus, all filenames containing a t are printed. Because there are no files ending with x, no substitution occurs in the last case. Therefore, the echo command simply displays *x.

### Matching Single Characters

The asterisk (*) matches zero or more characters, meaning that *x* matches the file x as well as x1, x2, xabc, and so on. The question mark (?) matches exactly one character. So cat ? will display all files that have filenames of exactly one character, just as cat ?x prints all files with two-character names beginning with x. Here we see this behavior illustrated again with echo:

```sh
$ ls
a
aa
aax
alice
b
bb
c
cc
```
