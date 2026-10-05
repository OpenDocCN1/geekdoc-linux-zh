# TUTORIAL: USING vim TO CREATE AND EDIT A File 189

![](bbox=[0.345, 0.103, 0.758, 0.345])

Figure 5-18 Modes in vim

vim is case When you give vim a command, remember that the editor is case sensitive other words, vim interprets the same letter as two different commands, depending sensitive on whether you enter an uppercase or lowercase character. Beware of the CAPS LOCK (SHIFTLOCK) key. If you set this key to enter uppercase while you are in Input mode and then exit to Command mode, vim interprets your commands as uppercase letters. It can be confusing when this happens because vim does not appear to be executing the commands you are entering.

# ENTERING TEXT

I/a (Input mode) When you start, you must put it in Input mode before you can enter text. To put vim in Input mode, press the i (insert cursor) or the a (append after cursor) key.

If you are not sure whether vim is in Input mode, press the ESCAPE key; vim returns to Command mode if it was in Input mode or beeps, flashes, or does nothing if it is already in Command mode. You can put vim back in Input mode by pressing the i or a key.

While vim is in Input mode, you can enter text by pressing the keyboard. The text does not appear on the screen as you type, vim is not in Input mode.

To continue with this tutorial, enter the sample paragraph shown in Figure 5-19 (next page), pressing the RETURN key at each end of line. If you do not return before the cursor reaches the right of the screen or window, vim wraps the text so that it starts a new line. Physical lines will not correspond to programming (logical) lines in this, so editing will be more difficult. While you are using vim, you can always correct any typing mistakes you make. If you notice a mistake on the line you are entering, you can correct it before you finish (page 190). You can correct other mistakes later. When you finish entering the paragraph, press ESCAPE to return vim to Command mode.