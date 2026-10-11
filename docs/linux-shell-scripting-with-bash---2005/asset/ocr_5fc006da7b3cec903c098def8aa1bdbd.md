# # File Statistics

The Linux `wc` (word count) command provides statistics about a file. By default, `wc` shows the size of the file in lines, words, and characters. To make `wc` useful in scripts, switches must be used to return a single statistic.

The `-bytes` (or `-c` or `-C`) switch returns the file size, the same value as the file size returned by `stat`\`fsize`.

```
$ `wc -bytes invoices.txt`
20411 invoices.txt
```

To use `wc` in a script, direct the file through standard input so that the filename is suppressed.

```
$ `wc -bytes < status_log.txt`
57496
```

The `-lines` (or `-1`) switch returns the number of lines in the file. That is, it counts the number of line feed characters.

```
$ `wc -lines < status_log.txt`
1569
```

The `-max-line-length` (or `-L`) switch returns the length of the longest line. The `-words` (or `-w`) switch counts the number of words in the file.

`wc` can be used with variables when their values are printed into a pipeline.

```
$ `declare -r TITLE='Annual Grain Yield Report'`
$ `printf "%s\n" "$TITLE" | wc -words`
4
```

# # Cutting

The Linux `cut` command removes substrings from all lines contained in a file.

The `-fields` (or `-f`) switch prints a section of a line marked by a specific character. The `-delimiterr` (or `-d`) switch chooses the character. To use a space as a delimiter, it must be escaped with a backslash or enclosed in quotes.

```
$ `declare -r TITLE='Annual Grain Yield Report'`
$ `printf "%s\n" "$TITLE" | cut -d ' ' -f2`
Grain
```

In this example, the delimiter is a space and the second field marked by a space is `Grain`. When cutting with `printf`, always make sure a line feed character is printed; otherwise, `cut` will return an empty string.

Multiple fields are indicated with commas and ranges as two numbers separated by a minus sign (-).

```
$ `printf "%s\n" "$TITLE" | cut -d ' ' -f 2,4`
Grain Report
```