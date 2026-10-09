
## In the next group of exercises, you will use the change command.

### 11. In this exercise, you will change one small word forward with `<cw>`.

- a. Open vi with the file *nowtime*.
- b. Press `<G>` to move the cursor to the bottom line of the file.
- c. Press `<2W>` (two big words forward). The cursor will be on the word "*know*".
- d. Press `<cw>` (change small word forward). Your screen should look like Figure 12-17. Note that most versions of vi mark the point where the change will begin with the underscore and mark the point where the change will end with the $ (if your version doesn’t mark the change command this way, see the Hint that follows.)

```
What time is it?
I don`t kno$. But the moon is bright tonight.
```

**Figure 12-17 vi Marks the Impending Change to “know”**

- e. Type *care*
- f. Press `<Esc>`. Your screen should look like Figure 12-18.

```
What time is it?
I don`t care. But the moon is bright tonight.
```

**Figure 12-18 “know” Changed to “care”**

The command `<cw>` changes one *small* word. The period at the end of the sentence is itself a small word; it was not included in the change.

With some versions of vi, when you use the change command, your screen will look like Figure 12-19. The object you intend to change is removed, and vi waits for you to enter the new text. The change is not marked with the $. But the end result is the same.

![](img/cc8b9fd5970716027fba0d0a45c13900_225_0.png)

**Figure 12-19 This vi Screen Does Not Mark the Change Command with $**

### 12. In this exercise, you will change one big word forward with `<cW>`.

- a. Press `<3k>` (three lines up). Your cursor should be on the “t” of “time” in the sentence “Now is the time.”
- b. Press `<4W>` (four big words forward) to move the cursor to the “n” of “now.”
- c. Press `<cW>` (change one big word forward).
- d. Type *new!*
- e. Press `<Esc>` Your screen should look like Figure 12-20.

![](img/cc8b9fd5970716027fba0d0a45c13900_225_1.png)

**Figure 12-20 “now,” Changed to “new!”**

`<cW>` means “change a big word.” Big words include attached punctuation marks.

> Question: What variation of the change command could you have used instead of `<cW>` to make the change from “now.” to “new!”? The answer follows Exercise 15.

### 13. In this exercise, you will change one sentence forward with `<c>`.

- a. Press `<2j>` to move the cursor down two lines.
- b. Press `<0>` (the number 0) to move the cursor to the beginning of the line. Your cursor should be resting on the first character of the sentence “What time is it?”
- c. Press `<c>`.
- d. Type *Where are we?*
- e. Press `<Esc>`. Your screen should look like Figure 12-21.

```
Now is the time. The time is new! Is it time yet?
Where are we?
I don't know. But the moon is bright tonight.
```

**Figure 12-21 *noughtime* after Changing One Sentence with `<c>`**

### 14. In this exercise, you will change one sentence back with `<c>`. Your cursor should be resting on the “?” in “Where are we?”.

- a. Press `<c>`.
- b. Type *What time zone?*
- c. Press `<Esc>`.

### 15. In this exercise, you will change two small words forward with `<2cw>`.

- a. Press `<1G>` (number 1, not letter “l”) to move to the first character of the file.
- b. Press `<w>` to move forward one small word.
- c. Press `<2cw>` (change 2 small words forward).
- d. Type *it is*
- e. Press `<Esc>`
- You replaced six characters (“is the”) with five characters (“it is”).
- *vi* removed the extra space. (Remember that a space is a character.)

> Answer to the question we posed at the end of Exercise 12: `<2cw>` vi sees “now:” as either two small words or one big word.

### 16. In this exercise, you will change three small words back with `<3b>`.

- a. Press `<5e>` to move the cursor to the n of men.
- b. Press `<l>` to move the cursor one character to the right.
- c. Press `<3cb>` (change 3 small words back).
- d. Type *most nice guys*
- e. Press `<Esc>`

Two things to note: (1) `<cb>` does not change the character under the cursor. That is why you moved the cursor one character to the right before you made the change. (2) The new phrase, “most nice guys,” has one character more than the phrase it replaced. vi made room for the extra character.

### 17. In this exercise, you will change one line with `<cc>`.

- a. Press `<G>` to move the cursor to the last line of the file.
- b. Press `<cc>` (change entire line).
- c. Type *We are on the last line of this file.*
- d. Press `<Esc>`
- e. Press `<u>` to restore the text you just changed.

## In the next group of exercises, you will delete text.

### 18. Before you begin this series of exercises, start with a “clean slate” by reloading *nowtime*.

- a. Press `<:e>`
- b. Press `<Space Bar>`
- c. Type *nowtime*
- d. Press `<Enter>`

vi gives you a warning on the status line: “No write since last change (use ! to override)”. vi is reminding you that you have changed the current file and have not saved the changes. You don't want to save the changed file.

- e. Press `<sel>`. The exclamation point tells vi to “load anyway.”
- f. Press `<Space Bar>`
- g. Type **notwime**
- h. Press `<Enter>`

### 19. In this exercise, you will delete words.

- a. Press `<1G>` to move the cursor to the first character in the file.
- b. Press `<dw>` to delete one small word. Your screen should look like Figure 12-22.

```
is the time for all good men to come to the
aid of their country.  Now is the time for all
```

**Figure 12-22 notwime after Deleting One Small Word with `<dw>`**

- c. Press `<u>` to undo the deletion.
- d. Press `<4w>` to delete four small words. Your screen should look like Figure 12-23.

```
for all good men to come to the
aid of their country.  Now is the time for all
```

**Figure 12-23 notwime after Deleting Four Small Words with `<4w>`**

- e. Press `<u>` to undo the deletion.
- f. Press `<3j>` (down three lines) to move the cursor to the line that begins “Now is the time.”
- g. Press `<3w>` (three small words forward) to move the cursor to the letter “t” of “time.”
- h. Press `<dw>` to delete one small word. Note that the period remains. It is a separate small word. Your screen should look like Figure 12-24.

```
Now is the . The time is now. Is it time yet?
What time is it?
I don't know. But the moon is bright tonight.
```

![](img/cc8b9fd5970716027fba0d0a45c13900_229_0.png)

- i. Undo the deletion.
- j. Press `<dW>` to delete one big word. This time the period is deleted. Your screen should look like Figure 12-25.

```
Now is the The time is now. The time is
What time is it?
I don't know. But the moon is bright tonight.
```

![](img/cc8b9fd5970716027fba0d0a45c13900_229_1.png)

- k. Undo the deletion.
- l. Press `<W>` (big word forward) to move the cursor to the word "The".
- m. Press `<db>` to delete a small word back. Your screen should look like Figure 12-26.

```
Now is the timeThe time is now. Is it time yet?
What time is it?
I don't know. But the moon is bright tonight.
```

![](img/cc8b9fd5970716027fba0d0a45c13900_229_2.png)

- n. Undo the deletion.
- Be certain the cursor is positioned on the first letter of “The” before doing the next step.
- o. Press `<dB>` to delete one big word back. Your screen should look like Figure 12-27.

```
Now is the The time is now.  Is it time yet?
What time is it?
I don't know.  But the moon is bright tonight.
```

**Figure 12-27 *nowtime* after Deleting with `<dB>`**

- p. Undo the deletion.

### 20. In this exercise, you will delete to the beginning and the end of the sentence.

- a. Position the cursor on the period at the end of the sentence “Now is the time.”
- b. Press `<dS>` to delete to the end of the line. Your screen should look like Figure 12-28.

```
Now is the time
What time is it?
I don't know.  But the moon is bright tonight.
```

**Figure 12-28 Deleting to the End of the Sentence with `<dS>`**

You see that vi deletes from the cursor position to the end of the sentence. The cursor was on the period, and the period is gone.

- c. Undo the deletion. Be certain that the cursor is back on the period after “time.”
