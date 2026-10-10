```
$ whereis grep<Enter>
find: /bin/grep /usr/share/man/man1/grep.1.gz
```

whereis has also substantiated the results of the which search results. Sancho correctly perceives that there is only one executable grep, which is common to ordinary users and root users.

# Locating Data within a File: grep Command

You can use the grep (global regular expression parsing) command alone or with other commands. We mentioned this command in Chapter 7, "Shell Basics," in the discussion of commands that are used as filters to other commands. The syntax for the basic use of grep looks a lot like the syntax for any command:

```
$ grep [options] regular expression [filename1 filename2 ... filenameN]
<Enter>
```

There is another syntax for grep for those occasions when grep is used in tandem with other commands. That syntax is as follows:

```
$ commandname [options] | grep [options] | commandname [options]<Enter>
```

or

```
$ commandname [options] | grep [options]<Enter>
> | commandname [options]<Enter>
```

We showed the tandem commands earlier as they would typically be typed: on two separate lines. By the time you enter three or more commands, you have probably decided to split them (to type part of the command structure at the primary prompt and the rest at the secondary prompt).

Generally, the grep command searches for a regular expression, a specified pattern of text, logical constructs, and/or metacharacters (patterns or wildcard symbols that stand for something special) within specified files. If and when such expressions are found, grep takes one or more slices (each line in the text file that contains the regular expression is a slice) from the files and writes the slices to stdout.