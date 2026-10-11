![](bbox=[0.21, 0.1, 0.6, 0.3])

**Figure 5-4** grep searches for a string

The `grep` command in Figure 5-4 searches through the file `memo` for lines that contain the string `credit` and displays a single line that meets this criterion. If `memo` contained such words as `discredit`, `creditor`, or `accreditation`, `grep` would have displayed those lines as well because they contain the string it was searching for. The `→w` option causes `grep` to match only whole words. Although you do not need to enclose the string you are searching for in single quotation marks, doing so allows you to put `SPACES` and special characters in the search string.

The `grep` utility can do much more than search for a simple string in a single file. Refer to the `grep` info page and Appendix A, “Regular Expressions,” for more information.

# head: Displays the Beginning of a File

By default the `head` utility displays the first ten lines of a file. You can use `head` to help you remember what a particular file contains. For example, if you have a file named `months` that lists the 12 months of the year in calendar order, one to a line, then `head` displays `Jan` through `Oct` (Figure 5-5).

This utility can display any number of lines, so you can use it to look at only the first line of a file, at a full screen, or even more. To specify the number of lines displayed, include a hyphen followed by the number of lines in the `head` command. For example, the following command displays only the first line of `months`:

```
$ head -1 months
Jan
```

The `head` utility can also display parts of a file based on a count of blocks or characters rather than lines. Refer to the `head` info page for more information.

# tail: Displays the End of a File

The `tail` utility is similar to `head` but by default displays the *last* ten lines of a file. Depending on how you invoke it, this utility can display fewer or more than ten lines, use a count of blocks or characters rather than lines to display parts of a file,