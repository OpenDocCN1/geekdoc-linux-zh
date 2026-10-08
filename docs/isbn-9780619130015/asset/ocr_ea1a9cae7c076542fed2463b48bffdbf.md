| Command | Purpose |
|---|---|
| x | Delete the character at the cursor |
| dd | Delete the current line |
| dw | Delete the word starting at the cursor. If the cursor is in the middle of the word, delete from the cursor to the end of the line. |
| d$ or D | Delete from the cursor to the end of the line |
| d0 | Delete from the cursor to the start of the line |

Table 3-2: vi editor's delete commands

Now you can use the delete commands and the cursor movement keys to edit text you inserted in your memo.

# **To edit the temp file by deleting text:**

+   1. Press Esc to make sure you are in command mode.
2. Type 1G to move to the first line of the file. You want to delete this line.
3. To delete the first line, type dd.
   Your file should now look like Figure 3-5.

![](bbox=[0.21, 0.58, 0.78, 0.93])

Figure 3-5: Memo after deleting first line