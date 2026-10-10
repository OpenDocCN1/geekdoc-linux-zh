data to the state it was in before you cut it.

The Emacs editor also includes a fancy way of mass-cutting text. Just move the cursor to the start of the area you want to cut, and press either the C-@ or C-spacebar keys. Then move the cursor to the end of the area you want to cut, and enter c-w. All the text between the two locations is cut.

# ## Copying and pasting

You've seen how to cut data from the Emacs buffer area; now it's time to see how to paste it somewhere else. Unfortunately, if you use the vim editor, this process may confuse you when you use the Emacs editor.

In an unfortunate coincidence, pasting data in Emacs is called *yanking*. In the vim editor, copying is called yanking, which is what makes this a difficult thing to remember if you happen to use both editors.

After you cut data using one of the cut commands, move the cursor to the location where you want to paste the data, and use the c-y command. This yanks the text out of the temporary area and pastes it at the current cursor position. The c-y command yanks the text from the last cut command. If you've performed multiple cut commands, you can cycle through them using the M-y command.

To copy text, just yank it back into the same location you cut it from and then move to the new location and use the c-y command again. You can yank text back as many times as you desire.

# ## Searching and replacing

Searching for text in the Emacs editor is done by using the c-s and c-r commands. The c-s command performs a forward search in the buffer area from the current cursor position to the end of the buffer, whereas the c-r command performs a backward search in the buffer area from the current cursor position to the start of the buffer.

When you enter either the c-s or the c-r command, a prompt appears