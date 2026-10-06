```
$1 ~ /^\/ { print $0 > "symlinks.txt" }
```

Here we see a program that writes separate lists of regular files, directories, symbolic links.

AWK provides a >> operator for appending to files, but since AWK only opens a file per program execution, the > causes AWK to open the file at the beginning of execution and truncate the file to zero length much like we see in the shell. However, once the file is open, it stays open and each subsequent write appends contents to the file. The >> operator behaves in the same manner, when the file is initially opened it is not truncated and all content is appended (i.e., it preserves the contents of an existing file).

AWK also allows output to be sent to pipelines. Consider this program, where we read our directory into an array and then output the array:

```
ls -1 /usr/bin | awk '
$1 ~ /^/ { a[$9] = $5
END (for i in a)
print a[i] "\t" i }
```

If we run this program, notice that the array is output in a seemingly random “implementation dependent” order. To correct this, we can pipe the output through sort:

```
ls -1 /usr/bin | awk
$1 ~ /^/ { a[$9] = $5
END (for i in a)
print a[i] "\t" i | "sort -nr"
}
```

# Reading Data

As have seen, AWK programs most process data supplied from standard input. However, we can also specify input files on the command line:

```
awk 'print $0' file1 file2 file3
```

Knowing this, we can, for example, create an AWK program that simulates the cat command:

```
or wc:
awk '{chars += length($0); words += NF}
END {print NR, words, chars}' file1
```

This program has a couple of interesting features. First, it uses the AWK string function length to obtain the number of characters in a string. This is one of many functions that AWK provides, and we will talk more about them in a bit. The second feature is the chars + NR expression at the end. This is done because length($0) does