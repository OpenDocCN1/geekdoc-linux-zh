If multiple files are specified, the contents of the files are concatenated in the output, but line numbering is restarted at 1 for each file. As an illustration, the following command.

```
$ cat -b fruits users
```

produces the output

```
1 Fruit Price/lbs Quantity
2 Banana $0.69 100
3 Peach $0.79 65
4 Kiwi $1.50 22
5 Pineapple $1.29 35
6 Apple $0.99 78

1 ranga
2 vathsa
3 amna
```

# WC

Now let's look at getting some information about the contents of a file. Using the wc command (short for word count), we can get a count of the total number of lines, words, and characters contained in a file. The basic syntax of this command is:

```
wc [opts] files
```

Here opts are one or more of the options given in Table 3.1, and files are the files you want examined. The options, opts, are optional and can be omitted.

# TABLE 3.1 wc Options

| Option | Description |
|---|---|
| -l | Count of the number of lines. |
| -w | Count of the number of words. |
| -m | Count of the number of characters. This option is available on Mac OS X, OpenBSD, Solaris, and HP-UX. This option is not available on FreeBSD and Linux systems. |
| -c | Count of the number of characters. This option is the Linux and FreeBSD equivalents of the -m option. |

When no options are specified, the default behavior of wc is to print out a summary of the number of lines, words, and characters contained in a file. For example, the command

```
$ wc fruits
```