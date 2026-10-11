# Copy-editing the vi way

The `vi` text editor has a wealth of editing commands that make changing whatever you type into your text a breeze. All these commands require that you place `vi` in the command mode by pressing `Esc`; otherwise, you insert all the commands that you type into your text. Table B-7 contains text-editing commands. (Make sure that you replace *n* with an actual number.)

**Table B-7 Text-Editing Commands**

| Command | What It Does |
| :--- | :--- |
| nX | Deletes *n* (meaning a number that you specify) characters beginning with the character at the cursor. |
| nShift+X | Deletes *n* characters backward from the character at the cursor. |
| Shift+D | Deletes the line from the cursor to the end of the line. |
| dW | Deletes the word at the cursor position. |
| dD | Deletes the line on which the cursor sits. |
| Shift+J | Combines the line on which the cursor sits with the next line. The next line goes at the end of the current line. |
| . (period) | Repeats the previous editing command. |

# Cut and paste text without scissors and glue

You're probably familiar with the cut-and-paste features of Macs and PCs running Windows. You highlight the text that you want to cut, select Cut from the Edit menu, and the text disappears from the screen. Then you move the cursor to the spot in your text where you want to insert the text and select Paste from the Edit menu. Right before your eyes, the text that disappeared appears again.

The `vi` text editor has similar features known as *yank* and *put*. *Yank* is the same as Cut and *put* is the same as Paste in Windows. Table B-8 contains the *yank* and *put* commands. (Remember to replace *n* with a number.)