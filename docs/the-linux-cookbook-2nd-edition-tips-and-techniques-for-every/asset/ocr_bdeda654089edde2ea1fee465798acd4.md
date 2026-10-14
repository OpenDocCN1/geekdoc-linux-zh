Emacs outputs the number of lines per page of the current buffer in the echo area.

For example, suppose the output in the minibuffers is this:

```
Page has 351 lines (69 + 283)
```

This means that the current page contains 351 lines, and point is on line number 70—there are 69 lines before this line and 283 lines after it.

# 12.1.4 Counting the Occurrences of Something

To find the number of occurrences of a text string or pattern in a file or files, use grep to search the file(s) for the text string, and pipe the output to wc with the -l option.

Here are two ways to use this.

+   - To find the number of lines in the file outline that contain the string “chapter,” type:
+     $ grep chapter outline | wc -l RET

+   - To find the number of lines in all of the files with a .txt extension in the /usr/share/doc/ directory tree that contain the string “chapter,” regardless of case, type:
+     $ grep -r -i chapter /usr/share/doc/ | wc -l RET

NOTES: This method is quick and easy, but it will not count more than one occurrence on the same line, and it won’t find occurrences that are broken by the end of a line.

For more recipes for searching text, and more about grep, see Chapter 14 [Searching Text], page 333.

# 12.1.5 Counting a Selection of Text

A useful trick for counting how many words are in some text you see displayed in some window or terminal—say, displayed in a Web browser—is to select the text (see Recipe 10.3 [Manipulating Selections of Text], page 253), and then count it as follows: run wc in another terminal, paste the text selection into this terminal, and then type CTRL-D to end the input. It will give a count for the selection.