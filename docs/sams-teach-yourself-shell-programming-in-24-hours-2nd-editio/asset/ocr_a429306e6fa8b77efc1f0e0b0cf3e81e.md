By piping the output to head, you can get an idea of the ten most repeated words:

```
$ tr '!?";|\()[]{},.'\n' < ch15.doc | tr 'A-Z' 'a-z' | tr -s ' ' | tr ' ' '\n' | sort | uniq -c | sort -rn | head
```

```
369 the
104 to
127 of
115 is
115 and
111 a
80 files
70 file
69 in
65
```

# Sorting Numbers in a Different Column

In the preceding output, you used the sort -rn command to sort the output by numbers because the numbers occurred in the first column instead of the second. If the numbers occurred in any other column, this would not be possible. Suppose the output looked like the following:

```
$ cat switched.txt
files 80
file 70
is 115
and 115
a 111
in 69
' 65
the 369
to 104
of 127
```

Now you need to tell sort to sort on the second column; you cannot simply use the -r and -n options. You need to use the -k (short for key) option.

The sort command constructs a 'key' for each line in the file, and then it arranges these keys into sorted order. By default, the key spans the entire line. The -k option gives you the flexibility of telling sort where the key should begin and where it should end, in terms of columns. The number of columns in a line is the number of individual words (alphanumeric strings separated by a tab or space) on that line. For example, the following line contains three columns:

```
files 80 100
```

The basic syntax of the -k option is

```
sort -k start,end files
```