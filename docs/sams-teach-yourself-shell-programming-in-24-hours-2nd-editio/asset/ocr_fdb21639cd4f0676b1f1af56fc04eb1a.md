# Counting Words

To count the number of words in a file, the -w (as in words) option can be used. For example, the command

```
$ wc -w fruits
```

produces the output

18 hosts

The first number, in this case 18, is the number of words in the file. The name of the file is listed at the end of the line.

When multiple files are specified, the number of words in each file is listed along with the total number of words in all of the specified files. As an example, the command

```
$ wc -w fruits users
```

produces the output

18 fruits
3 users
21 total

# Counting Characters

To count the number of characters, we need to use either the -m or the -c option. The -m option is available on Mac OS X, OpenBSD, Solaris, and HP-UX. On FreeBSD and Linux systems, the -c option should be used instead.

For example, on Solaris the command

```
$ wc -m fruits
```

produces the output

219 fruits