# Table 19.19 **Common ispell flags (continued).**

| Flag | Purpose | Value |
|---|---|---|
| -T | Expects the file to be of the specified type, rather than getting it from the file name | A formatting type, such as rnof, troff, TeX, or LaTeX |
| -w | Lists characters that are not normally parts of words, but that you do not want **ispell** to complain about, such as $ | The character(s) in question, with no separation |
| -W | Lists a word length that is always legal | Number of characters long this word should be |
| -x | Does not create a backup file | None |

+   5. Choose whether you want **ispell**'s menu displayed at the bottom of the screen. If you do, then add the **-M** flag. If not, add **-N**. The menu contains the following, though the text is all on one line on the screen:

```
[SP] <number R)ep| A)cept I)nsert L)ookup U)ncap
Q)uit e(X)it or ? for help
```

In the example, perhaps you chose the menu. Now you have:

```
ispell -b -w $ -M
```

+   6. Determine whether you want additional lines of text to be displayed, to give context to the item **ispell** flags. If so, add the flag **-L** with the number of lines to include. To use four lines of context in the example, you would now have:

```
ispell -b -w $ -M -L4
```

+   7. Finally, add the file name at the end. In the example, you might now have:

```
ispell -b -w $ -M -L4 ~/sample.txt
```

+   8. The **ispell** program now steps through the file and displays all words that do not match its rules. Although the menu displays some of the commands you have available to you, the full list is given in Table 19.20.