The way you can monitor its state is by the shape of the text cursor in the edit window. The default is for Insert to be on. When Insert is on, the text cursor is a small flashing line. When Insert is off, the text cursor is a flashing block instead.

What does it do? The Insert toggle determines how newly typed characters are added to your work file. When Insert is on (that is, if the cursor is a flashing line), characters that you type are inserted into the file. The characters appear over the cursor and immediately push the cursor and the rest of the line to the make room for themselves. The line becomes one character longer for each character that you type. If you press Enter, the cursor moves down one line, carrying with it the part of the line lying to its right.

When Insert is off (that is, if the cursor is a flashing block), characters that you type will overwrite characters that already exist in the file. Assuming you're typing in the middle of the file, somewhere within a line, you will overwrite one character for every character that you type. Only if you overwrite existing characters all the way to the end of the line or the end of the file and keep typing will the total number of characters increase. If you press Enter, the cursor will move down to the first character of the next line down, but nothing else change. A line will only be added to the file if you press Enter with the cursor on the last line of the file.

Turning Insert on and off is done with a single control keypress:

Ctrl-V or Ins toggles Insert on and off.

# The Indent Toggle

Indent is another toggle. It indicates whether NASM-IDE's auto-indent feature is on or off. When Insert is on, the cursor will automatically move beneath the first visible character on a new line when you press Enter. In other words (assuming that the Indent is on), given this little bit of text on your screen:

```
Adjust:
MOV AX, [BP] + 6
SUB AX, Increment_ <--Before pressing Enter
```

| After pressing Enter