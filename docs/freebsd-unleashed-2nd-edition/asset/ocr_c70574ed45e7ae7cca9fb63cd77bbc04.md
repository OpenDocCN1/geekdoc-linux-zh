To start vi with an empty file, type vi. To start vi and load a file for editing, type vi followed by the filename. If the filename you specify doesn't already exist, vi will assume that this is a new file. Figure 6.4 shows a vi session with a new file ready for editing.

![](bbox=[0.2, 0.18, 0.8, 0.47])

**FIGURE 6.4** The vi editor, ready to edit a new file. The status line at the bottom of the screen gives information about the file being edited.

Looks rather plain and boring, doesn't it? One of the first things you may notice if you start trying to type text is that vi does nothing except beep at you; it doesn't insert any of the text you are typing. You may also hit certain keys and see strange-looking messages on the status line at the bottom of the screen. This is because vi has different modes of operation.

When vi first starts, it is in *command mode*. In command mode, keypresses are interpreted as commands to the editor rather than as text to be inserted into the document. To switch into the mode in which you can enter text into the document, you must press the a, i, or o key, depending on where you want the text to appear in the document:

+   * The a command stands for *append*. In this mode, the text you type will be inserted after whatever character the cursor is currently on.

+   * The i command stands for *insert*. In this mode, the text you type will be inserted before whatever character the cursor is currently on.

+   * Finally, the o command stands for *open*. This will cause a new line to be inserted after the line the cursor is currently on. Then, the cursor will move to the new line, and vi will enter insert mode, allowing you to enter text on the new line.