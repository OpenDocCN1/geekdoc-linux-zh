
## 3.3.5 Keystroke Macros

The emacs text editor contains a simple-to-use facility that allows you to define keystroke macros, or collections of keystrokes that can be recorded and then played back at any time. This capability allows you to define repetitive multiple keystroke operations as a single command and then execute that command—as many times as you want. The keystrokes can include emacs commands and a series of keystrokes. A macro can also be saved with a name, or even be saved to a file, for use during subsequent emacs editing sessions. Table 3.15 shows a list of some of the most important keyboard macro commands.

For a more complete description and detailed explanation of how to record, edit, list, and delete keystroke macros, see Section 3.3.13.5.

Practice Session 3.9 lets you create a new text file using some of the commands presented in Table 3.15.

### 3.3.5.1 Practice Session 3.9

Step 1: At the shell prompt, type emacs datafile and then press <Enter>.

The emacs screen appears on your display.

Step 2: Hold down <Ctrl+X> <Shift+9>. These actions begin your keyboard macro definition. If you make a mistake anywhere in subsequent steps, simply hold down <Ctrl+G> to cancel the current macro definition.

Step 3: Type 1 2 3 4 5 6 7 8 9 10 and then press <Enter>.

Step 4: Hold down <Ctrl+X> <Shift+0>. These actions end your macro definition.

Step 5: Hold down <Ctrl+X> e. Doing so replays the macro that you just defined, placing another line of the numbers 1 through 10 in the buffer.

Step 6: Repeat Step 5 eight more times so that your display looks similar to that shown in Figure 3.8.

Step 7: Hold down <Ctrl+X> <Ctrl+S>. These actions save the buffer to the file datafile.

Step 8: Hold down <Ctrl+X> <Ctrl+C> to exit from emacs.

![](img/02e070097d401d3bf7de4bf1c470b267_146_0.png)

FIGURE 3.8 Display after Step 6.

## 3.3.6 Cut or Copy and Paste and Search and Replace

As we mentioned previously, every word processor has the capability to cut or copy text and then paste that text back into the document and to search for old text and replace it with new text. Because emacs operations can be totally text activated, whereby you use sequences of keystrokes to execute commands, cutting or copying and pasting are fairly complex operations. They are accomplished with the Kill Ring, whereby text is held in a buffer by killing it and is then restored to the document at the desired position by yanking it. Global search and replace are somewhat less complex and are accomplished by either an unconditional replacement or an interactive replacement.

The mark is simply a place holder in the buffer. For example, to cut three words from a document and then paste them back at another position, move the point before the first word you want to cut and press <Esc+c+D> three times. The three words are then cut to the Kill Ring. Because the Kill Ring is a FIFO buffer, you can now move the point to where you want to restore the three words and press <Ctrl+y>. The three words are yanked into the document in the same order, left to right, that they were cut from the document.

To copy three words of text and then paste them back at another position, set the mark by positioning the point after the three words, and then press <Ctrl+@> at that position. Then reposition the point before the three words; you have now defined a region between the point and the mark. There is only one mark in the document. Press <Esc+w> to send the text between the point and the mark to the Kill Ring; the text is sent, but it is not blanked from the screen display. To restore the three words at another position, move the point there and press <Ctrl+y>. The three words are restored at the new position. Table 3.13 gives the important kill and yank commands for emacs.

Global search and replace can be either unconditional, where every occurrence of old text you want to replace with new text is replaced without prompting, or it can be interactive, where you are prompted by emacs before each occurrence of old text is replaced with new text. Also, the grammar of replacement can include regular expressions, which we do not cover here.

For example, to replace the word men unconditionally with the word women from the current position to the end of the document, press <Esc+x>, type replace-string, and then press <Enter>. You are then prompted for the old string. Type men and then press <Enter>. You are then prompted for the new string. Type women and then press <Enter>. All occurrences are replaced with no further prompts.

To accomplish an interactive replacement, simply press <Esc+x>, type query-replace, and then press <Enter>. You can then input old and new strings, but you are given an opportunity at each occurrence of the old string to replace it or not to replace it with the new string. Table 3.14 shows the actions that you can take while in the midst of an interactive search and replace. Practice Session 3.10 contains further examples of copying and pasting and global search and replace, both unconditional and interactive. Your objective will be to type in one line of text, copy it into the Kill Ring, and then paste it into the document seven times. Then modify the contents of the original line and each pasted line by using both interactive search and replace and unconditional search and replace. Upon completion of Practice Session 3.10, your screen display should look similar to Figure 3.9.
