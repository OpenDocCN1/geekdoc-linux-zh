The line numbers appear on the screen but are not written into the work buffer or the file.

This causes line numbers to be placed down the left-hand margin:

```
```
1  Poem #1
2  Mary had a little lamb,
3  A little cheese,
4  A little ham.
5  Delicious!
6
7  Poem #2
8  Mary had a polar bear
9  Whose fur was white as snow,
10 And everywhere that big bear went
11 The people let it go.
```
```

Although the line numbers appear on the screen, they are not actually put into the work buffer or into the file.

+   3.  **To remove the line numbers, enter the Set No Numbers command.** This must be done in the command mode:
+   
+       `:set nonu` (Return)

# ### 12.7 Yanking and Putting

You may occasionally need to move large blocks of text around within a file or between two different files. This is done by copying the text temporarily into one of the named or numbered buffers. Recall there are 26 named buffers and 9 numbered buffers:

+   *   Named buffers "a", "b", "c", . . . , "z"
+   *   Numbered buffers "1", "2", "3", . . . , "9"

In UNIX vocabulary, “yanking” is the process of copying text into a named or numbered buffer; “putting” is the process of copying the text back out again.

+   1.  **Use vi to open the file.** If you have been following the examples thus far, open the file *poems*.
+   2.  **In the command mode, move the cursor to the first of the lines you wish to copy.** To copy the second poem, move the cursor to the first line of the poem:
+       `Mary had a polar bear`
+   3.  **Yank the lines into a named buffer.** Thus, to copy four lines into named buffer "a, type the following line (no `Return` is required):
+       `"a4yy`

This does not appear on screen.

This command line is best interpreted backwards. It yanks (`yy`) four lines of text (4) and places them in the named buffer "a. Although the command itself