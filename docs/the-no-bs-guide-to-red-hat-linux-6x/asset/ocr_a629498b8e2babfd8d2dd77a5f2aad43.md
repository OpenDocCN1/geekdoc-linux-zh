away. To delete the blank line from the file, press CTRL-K again or press the DEL key.

# CUTTING AND PASTING WITH EMACS

If you ever want to move a block of text from one spot in your file to another, you can use CTRL-K (kill) along with CTRL-Y (yank) to get the job done. When you press CTRL-Y, the last thing you “killed” with CTRL-K will be yanked back into the file. So to move a block of text, just kill one or more lines with CTRL-K, then put your cursor at the spot where you’d like to place the text and press CTRL-Y to yank it back.

For example, here’s how to move the first line of the bulb.joke file to the end. With your cursor on the first character of the first line, press CTRL-K twice. (Line 1 disappears.) Press the down arrow twice to move your cursor to the third line of the file, which is now blank. Press CTRL-Y once to paste the deleted line at line 3 and then press CTRL-Y again.

You should now have two copies of the deleted line at the end of your file, which should look like Figure 7-5.

```
A: Two--one to hold the giraffe, and the other to fill the
bath tub with brightly colored machine tools.
Q: How many surrealists does it take to change a light bulb?
Q: How many surrealists does it take to change a light bulb?

--**Emacs: bulb.joke    (Fundamental)--All----------------
```

Figure 7-5: Entering text with Emacs