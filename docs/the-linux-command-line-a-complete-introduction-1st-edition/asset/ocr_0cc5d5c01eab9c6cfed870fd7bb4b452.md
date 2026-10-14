# Table 19-1 (continued)

| Option | Description |
| --- | --- |
| -l | Print the name of each file that contains a match instead of the lines themselves. May also be specified --files-with-matches. |
| -L | Like the -l option, but print only the names of files that do not contain matches. May also be specified --files-without-match. |
| -n | Prefix each matching line with the number of the line within the file. May also be specified --line-number. |
| -h | For multfile searches, suppress the output of filenames. May also be specified --no-filename. |

In order to more fully explore grep, let’s create some text files to search:

```
[me@linuxbox ~]$ ls /bin > dirlist-bin.txt
[me@linuxbox ~]$ ls /usr/bin > dirlist-usr-bin.txt
[me@linuxbox ~]$ ls /sbin > dirlist-sbin.txt
[me@linuxbox ~]$ ls /usr/sbin > dirlist-usr-sbin.txt
[me@linuxbox ~]$ ls dirlist*.txt
dirlist-bin.txt  dirlist-sbin.txt  dirlist-usr-sbin.txt
dirlist-usr-bin.txt
```

We can perform a simple search of our list of files like this:

```
[me@linuxbox ~]$ grep bzip dirlist*.txt
dirlist-bin.txt:bzip2
dirlist-bin.txt:bzip2recover
```

In this example, grep searches all of the listed files for the string bzip and finds two matches, both in the file dirlist-bin.txt. If we were interested in only the files that contained matches rather than the matches themselves, we could specify the -l option:

```
[me@linuxbox ~]$ grep -l bzip dirlist*.txt
dirlist-bin.txt
```

Conversely, if we wanted to see a list of only the files that did not contain a match, we could do this:

```
[me@linuxbox ~]$ grep -L bzip dirlist*.txt
dirlist-bin.txt
dirlist-usr-bin.txt
dirlist-usr-sbin.txt
```

# Metacharacters and Literals

While it may not seem apparent, our grep searches have been using regular expressions all along, albeit very simple ones. The regular expression bzip is