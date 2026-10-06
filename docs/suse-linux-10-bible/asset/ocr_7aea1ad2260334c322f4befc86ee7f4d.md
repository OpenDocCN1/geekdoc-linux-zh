# Working with Fields from Text Files

The commands discussed in this section enable you to work with text files in which each line is regarded as being made up of a number of fields separated by white space or a particular delimiter character.

# cut

If you have a file that consists of lines of text that are split into fields by white space or a delimiter character, cut can get a particular field or fields from every line of the file. For example, in /etc/passwd the file is delimited by the colon character (:). The cut option -f tells it which field or fields you are selecting, and the -d option tells it what delimiter character. The file /etc/passwd is made up of lines like this:

```
user:x:1001:100:Guest User:/home/user:/bin/bash
```

To get just the real name (the fifth) and the shell (the seventh) fields from the file, you could do this:

```
user@bible:~ cut -d -f5,7 /etc/passwd
```

This would produce many lines of output like this:

```
Guest User:/bin/bash
```

You can also select particular characters from each line, using the -c option:

```
user@bible:~ cut -c2-4 file
first
second
third
fourth
irs
eco
hir
our
```