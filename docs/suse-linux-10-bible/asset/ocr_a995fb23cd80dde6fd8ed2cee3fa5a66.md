# Chapter 11 + Text Editors 315

![](bbox=[0.125, 0.133, 0.193, 0.178])

Note that the commands here are the default ones. The emacs editor is totally configurable, which means you can bind a particular keystroke to any command. For example, C-x C-f is bound to the command find-file, which you can also run with M-x find-file. You that breaking and binding the command to a different keystroke. You can also bind a keystroke to the command that you find yourself using regularly that has no binding (or one you find inconvenient). To make such a change, you need to add a line to your .gnu-emacs-custom file.

The most important emacs commands are as follows:

+   * C-x C-f — Find a file (that is, open).
* C-x C-b — Save the current buffer.
* C-x C-w — Write the current buffer to a file ("Save as").
* C-x C-c—Quit.
* C-k—Kill the rest of the current line.
* C-y— Yank (that is, copy) the last killed text.
* M-w—Copy the selected text.

# Moving Around

If you are using emacs in a graphical session, the mouse works both for selecting text and for moving around the file. But you can also navigate with the keyboard using the following keystrokes:

+   * C-f—Move to next character.
* C-b—Move to previous character.
* M-f—Move to next word.
* M-b—Move to previous word.
* C-a—Move to beginning of line.
* C-e—Move to end of line.
* M-a—Move to beginning of sentence.
* M-e—Move to end of sentence.
* C-Home—Move to top of buffer.
* C-End—Move to bottom of buffer.
* M-x goto-line—Move to a line number that you specify.