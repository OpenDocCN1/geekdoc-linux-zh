+   - In Command mode, move the cursor to the line you want to copy.
+   - Press yy. The line is copied into buffer 0 (the default buffer), but the original line remains on the screen. The cursor, meanwhile, stays where it was.
+   - Move the cursor to the line below which you want to place the yanked line.
+   - Press p. The yanked copy of the original line appears below the line where you placed the cursor. Now, the cursor moves to the newly placed (in other words, the copied) line.

As with moving text, if you want to do more complicated copying—say, copying several strings at once—do the following:

To copy a line into buffer 2, move the cursor to the line and type

```
"2yy
```

To copy a word into buffer 3, move the cursor to that word and type

```
"3yw
```

To copy a line and the three lines following it into buffer c, move to that line and type

```
"c4yy
```

Move to the various target locations and type "2p, "3p, and "cp, respectively, to place those text strings where you want them.

As with moving text, you can copy text repetitively or out of order because copies of the text strings remain in their respective buffers until they are replaced. In the multiple-copy example, just as in the multiple-move example (Example 10.2), "2yy, "3yw, and "c4yy are all preceded by one quotation mark. Remember, you must precede alphanumeric key combinations with one double quote when specifying buffers.

Meanwhile, notice that vi echoes, at the bottom of the screen, the actions you have taken (for example, xxx lines yanked; xxx more lines) as they are completed.

Example 10.3 illustrates a simple example of copying text.