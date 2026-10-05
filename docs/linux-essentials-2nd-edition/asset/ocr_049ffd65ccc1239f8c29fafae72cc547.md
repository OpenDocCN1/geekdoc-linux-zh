# Using cut

When extracting data, grep is helpful in pulling out entire file lines (sometimes called a *record*). Sometimes, though, you only need parts of a file record. The cut command can help in this case. It extracts text from fields in a file record. It's frequently used to extract variable information from a file whose contents are highly patterned.

To use cut, you pass to one or more options that specify what you want, followed by one or more filenames. For instance, users' home directories appear in the sixth colon-delimited field of the /etc/passwd file. Therefore, to extract only the directory name, use this command:

```
$ cut -f 6 -d ": /etc/passwd
```

Table 8.4 shows the options that you're most likely to need with the cut command. Consult its man page for additional options and a complete description of the cut command.

# TABLE 8.4 Common cut options

| Option (long form) | Option (short form) | Description |
| --- | --- | --- |
| --characters | -c | Selects only designated character position(s). |
| --delimiter | -d | Uses designated delimiter as field instead of the default (Tab). |
| --fields | -f | Selects only designated fields. |
| --only-delimited | -s | Lines without a delimiter are not printed (default is to print them when the -f option is used). |

You can capture the cut command's results into a file by using redirection. Redirection is covered later in this chapter, in the “Redirecting Input and Output” section.

# Using sort

When dealing with a large amount of data, being able to sort it is often useful. The sort command does just that. However, you need to be aware of its features in order to achieve the desired results.