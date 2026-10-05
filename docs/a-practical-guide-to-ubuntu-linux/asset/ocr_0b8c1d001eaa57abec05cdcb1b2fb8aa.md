# 166 CHAPTER 5 THE LINUX UTILITIES

```
$ cat memo

Helen:

 our meeting on June 6 we
discussed the issue of credit.
Have you had any further thoughts
about it?

Max

$ grep 'credit' memo
discussed the issue of credit.
```

**Figure 5-4** grep searches for a string

# grep: SEARCHES FOR A STRING

The grep utility searches through one or more files to see whether any contain a specified string of characters. This utility does not change the file it searches but simply displays each line that contains the string.

The grep command in Figure 5-4 searches through the file memo for lines that contain string credit and displays the single line that contains this criterion. If memo contained such words as discredit, creditor, or accreditation, grep would have displayed those lines as well because they contain the string it was searching. The -w (words) option causes grep to match only whole words. Although you do not need to include the string you are searching for in single quotation marks, doing so allows you to put spaces and special characters in the search string.

The grep utility can do more than search for a simple string in a single file. Refer to the grep info page and Appendix A, “Regular Expressions,” for more information.

# head: DISPLAYS THE BEGINNING OF A FILE

By default the head utility displays the first ten lines of a file. You can use head to help you remember what a particular file contains. For example, if you have a file named months that lists the 12 months of the year in calendar order, one to a line, then head displays Jan through Oct (Figure 5-5).

This utility can display any number of lines, so you can use it to look only the first line of a file, at a full screen, or even more. To specify the number of lines

+   1. Originally the name grep was a play on an ed—original UNIX editor, available on Ubuntu Linux—command: g/re/p. In this command g stands for global, re is a regular expression delimited by slashes, and p means print.