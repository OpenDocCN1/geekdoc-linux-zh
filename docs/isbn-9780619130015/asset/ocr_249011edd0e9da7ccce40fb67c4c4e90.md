![](bbox=[0.202, 0.09, 0.787, 0.423])

Figure 3-7: Completed memo after editing

The vi editor offers you alternatives for copying, cutting, and pasting text.

> Note: The delete line command, dd, actually places deleted lines in a buffer. Then you can use the paste command, p, to paste deleted (cut) lines elsewhere in the text. (Position the cursor where you want to paste them.) To copy and paste text, use the yank command, yy, to copy the lines. After yanking the lines you want to paste elsewhere, move the cursor and type p to paste the text in the current location.

# Undoing a Command

If you complete a command and then realize you want to reverse its effects, you can use the undo command. For example, if you delete a few lines from a file by mistake, type u to restore the text.

# Searching for a Pattern

You can search forward for a pattern of characters by typing a forward slash (/), typing the pattern you are seeking, and then pressing Enter. For example, suppose you want to know how many times you used the word “consist” or “consists” in your memo.