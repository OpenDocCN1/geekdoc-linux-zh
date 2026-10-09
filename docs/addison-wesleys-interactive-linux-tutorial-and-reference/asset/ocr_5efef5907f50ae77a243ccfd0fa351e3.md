changed the current file and have not saved the changes. You don't want to save the changed file.

+   e. Press <sel>. The exclamation point tells vi to “load anyway.”

+   f. Press <Space Bar>

+   g. Type **notwime**

+   h. Press <Enter>

+   19. In this exercise, you will delete words.

+   a. Press <1G> to move the cursor to the first character in the file.

+   b. Press <dw> to delete one small word. Your screen should look like Figure 12-22.

```
is the time for all good men to come to the
aid of their country.  Now is the time for all
```

**Figure 12-22 notwime after Deleting One Small Word with <dw>**

+   c. Press <u> to undo the deletion.

+   d. Press <4w> to delete four small words. Your screen should look like Figure 12-23.

```
for all good men to come to the
aid of their country.  Now is the time for all
```

**Figure 12-23 notwime after Deleting
Four Small Words with <4w>**

+   e. Press <u> to undo the deletion.

+   f. Press <3j> (down three lines) to move the cursor to the line that begins “Now is the time.”

+   g. Press <3w> (three small words forward) to move the cursor to the letter “t” of “time.”