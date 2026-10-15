# history

You will then see a complete history of the Last Line mode commands for this session at the bottom of the screen display.

Your entire search history for this session is displayed by typing history/ in Last Line mode.

<Ctrl+P> will work like the <Up> arrow key, except that it doesn't matter what you already typed. <Ctrl+N> works like the <Down> arrow key.

+   * The Last Line Mode Command Line Window

Typing any text in the Last Line mode command history to modify a previous command and then execute it is possible but difficult.

A better way to use a modified form of a Last Line mode command from the history is to open the command line window while in Command mode by typing:

# q:

Vim now opens a small utility window at the bottom of the screen. It contains the command line history and an empty line at the end, similar to this illustration:

```
+------------------------------------------------------------+
|other window |
|~ |
|:first.c==========================================|
|:w second.c |
|:w third.c |
|:w fourth.c |
|:w fifth.c |
|:w sixth.c |
|:history
|: |
|:command-line==================================|
||
~/project.c
+------------------------------------------------------------+
```

In the buffer in this small utility window, you are in Insert mode, and can use Insert mode commands to modify text and also move commands. You can use the arrow keys to move around.