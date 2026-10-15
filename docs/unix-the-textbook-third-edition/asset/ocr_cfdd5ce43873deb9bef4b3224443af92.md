The keystroke commands that you execute in vi are case sensitive; for example, uppercase A appends new text after the last character at the end of the current line, whereas lowercase a appends new text after the character the cursor is on.

To start vi, at the shell prompt, type vi (and optionally designate some option[s] and file name[s]) and then press <Enter>. You are now in Command mode. To enter Insert mode, type A and you are now able to insert text on the first line of the file.

After entering text, you can press the <Esc> key to enter Command mode.

At any point in your creation or manipulation of text, you can press the u key on the keyboard to undo the last operation.

From Command mode, you can save the text that you just inserted into the buffer to a file on disk by typing :w filename and pressing <Enter>, where filename is the name of the file you want to save the text to. To quit the editor, type :q.

# 3.2.3 The Format of a vi Command and the Modes of Operation

In Command mode, the generic syntax of keystrokes is:

```
[#1] operation [#2] target
```

where:

+   anything enclosed in [ ] is optional;

+   #1 is an optional number, such as 5, specifying how many operations are to be done;

+   operation is what you want to accomplish, such as deleting lines of text;

+   #2 is an optional number, such as 5, specifying how many targets are affected by the operation; and

+   target is the text that you want to do the operation on, such as an entire line of text.

Note that if the current line is the target of the operation, the syntax for specifying the target is the same as the syntax of the operation; for example, dd deletes the current line. Also, a variation on this generic syntax is the cursor movement command, whereby you can omit the numbers and operation and simply move the cursor by word, sentence, paragraph, or section. Table 3.2 lists some specific examples of this generic syntax and variations used in Command mode.

As previously stated, when you start vi, it is in Command mode. When you want to be in Insert mode instead of Command mode, press a valid key to accomplish the change. Some of these keys are shown in Table 3.3.

After inserting text, you can edit the text, move the cursor to a new position in the buffer, and save the buffer and exit the editor—all from within Command mode. When you want to change from Insert mode to Command mode, press the <Esc> key.

To save the buffer and exit the editor, press the : key (colon) to enter Last Line mode. The general commands that are useful in Last Line mode are shown in Table 3.4.