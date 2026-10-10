When the number of files to be located by find is relatively small.

No one really wants to sit at a terminal for a long time typing y and Enter or n and Enter repeatedly. This activity is tedious, and tedious activities can lead to mistakes.

Table 8.1 lists some other common options that you can specify with the find command. For even more options, consult your information sources.

# Example 8.3 find with an Interactive Action

Sancho is convinced now that his misc files should be deleted. He will use find in combination with a single action, but he will do it interactively. Doing it interactively is a good thing\u2014he is about to make a typographical error in his command sequence. But the interactivity will enable him to prevent the wrong files from being deleted:

```
$ find . -name 'm\*' -ok rm { } \;<Enter>
< rm ... ../mbox > ? n<Enter>
< rm ... ../misc > ? y<Enter>
< rm ... ./Misc/misc > ? y<Enter>
< rm ... ./Admin/memos > ? n<Enter>
< rm ... ./Admin/misc > y<Enter>
< rm ... ./Main/misc > ? y<Enter>
```

# Table 8.1 Selected find Options

| OPTION | DESCRIPTION |
| :--- | :--- |
| -type c | Find files of type c (character\u0002pecial file). The type can also be b (block special file), d (directory), f (plain file), l (symbolic link), p (fifo or a named pipe), or s (socket). |
| -size n[c] | Find files containing n blocks, or if c is specified, n characters long (1 block = 4,096 bytes) |
| -mtime +n\|n\|-n | Find files that were last modified more than (+n), less than (-n), or exactly (n) days ago |
| -perm nnn | Find files whose permissions are set to octal number nnn |
| -user username | Find files belonging to the specified user |
| -o | Find files that match specified conditions |
| -newer filename | Find files that have been modified more recently than filename. (Note the similarity to mtime.) |