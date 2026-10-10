$

Move the cursor to the beginning of the line:

```
0 (zero) .
```

+   8. Move your cursor to the top of the file.

```
1<Shift>-g
```

or

```
:1<Enter>
```

Search for the word *entry*. Your cursor should be on the *e*. Switch to Insert mode and add the word *text* with a space after the word.

```
/entry<Enter>
i
text
```

+   9. Move the cursor to the space after the word *mode* on the same line.
+       Insert a comma. Remember, you are still in Insert mode.

```
<Esc>
```

Position the cursor to the space after the word *mode*.

```
i
,
```

+   10. Enter Command mode. Position the cursor anywhere on the line
+        beginning with *learn the most*. Insert a blank line to form two
+        paragraphs.

```
<Esc>
```

Position the cursor on the line that starts with *learn the most*.