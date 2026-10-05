# Searching for Extracting Data

The result will be a listing of all files that have names ending in .c and reside within the /home directory tree.

# Using wc

A file's size in bytes, as revealed by ls or searched for using find, can be a useful metric. This size value isn't always the most useful for text files, though. You might need to know how many words or lines are in a text file—say, because you want to know how many pages a text document will consume when printed at 52 lines per page. The wc utility provides this information. For instance, to discover the information for a newly created file named newfile .txt in your working directory:

```
$ wc newfile.txt
37 59 1990 newfile.txt
```

This output reveals that the file.txt contains 37 lines, 59 words, and 1,990 bytes. By default, wc displays a count of words, and bytes for each file you pass to it.

You can pass options to limit or expand wc output, as summarized in Table 8.3. Of the options in Table 8.3, -l, -w, and -c are the defaults, typing wc file.txt is equivalent to typing wc -lw file.txt. The program's man describes more options, but the ones in Table 8.3 are the ones're most likely to use.

# TABLE 8.3 Common wc options

| Option (long form) | Option (short form) | Description |
|---|---|---|
| --bytes | -c | Displays the file's byte count |
| --chars | -m | Displays the file's character count |
| --lines | -l | Displays the file's newline count |
| --words | -w | Displays the file's word count |
| --max-line-length | -L | Displays the length of the longest line in the file |

Be aware that wc works correctly on plain-text files, but it may produce incorrect or even nonsensical results on formatted text files, such as HTML or word processor files. You're better off using a word processor or other specialized editor to find the number of words and other statistics for such files.

![](bbox=[0.751, 0.6265, 0.951, 0.8165])