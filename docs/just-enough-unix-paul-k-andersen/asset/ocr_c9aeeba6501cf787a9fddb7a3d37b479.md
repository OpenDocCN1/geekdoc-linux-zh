This runs `wc` on `out2.tmp` and `out3.tmp`, producing the output
```
4  27   133  out2.tmp
5  33   160  out3.tmp
9  60   293  total
```
Note that `wc` shows the line, word, and character counts for the files individually, as well as the totals for both files.

# 9.5 Using grep

The `grep` filter searches line by line through its standard input for a pattern of characters. Any line containing the desired pattern is printed on the standard output. The format of `grep` is
```
grep [-cinv] pattern [filelist]
```

The pattern may be a simple word or string of characters, or it may be a regular expression. A regular expression is a compact notation that specifies a general string of characters, in much the same way that a wildcard represents a set of file names. We will not use regular expressions in this book.

+   - **Search for a particular word in a set of files.** Thus, to search the files `out1.tmp`, `out2.tmp`, and `out3.tmp` for lines containing the word `tank`, you would use the command
+   ```
+   $ grep tank *tmp (Return)
+   ```
+   Any lines containing the pattern `tank` are listed on the screen:
+   ```
+   out2.tmp:My Bonnie looked into the gas tank,
+   out3.tmp:who drove around town in a tank.
+   ```

+   - **Search using the line-number option.** The `-n` option causes `grep` to print the number of any line containing the pattern:
+   ```
+   $ grep -n tank *tmp (Return)
+   ```
+   The word `tank` occurs on the first line of `out2.tmp` and on the second line of `out3.tmp`. Hence, grep prints
+   ```
+   out2.tmp:1:My Bonnie looked into the gas tank,
+   out3.tmp:2:who drove around town in a tank.
+   ```

+   - **Search using the list-only option.** This causes `grep` to list only the names of the files containing the pattern. For example,
+   ```
+   $ grep -l Bonnie *tmp (Return)
+   out2.tmp
+   ```