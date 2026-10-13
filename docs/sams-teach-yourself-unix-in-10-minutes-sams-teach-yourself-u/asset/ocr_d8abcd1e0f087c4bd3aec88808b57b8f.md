machine that you sit down in front of. Because of its ubiquity, knowing the basics of vi will enable you to work with your files even if there are no more-convenient editors available.

Follow these steps if you need to use vi:

+   1. Determine what file you want to edit.
+   2. Issue the vi command as `vi <filename>`. The vi editor can also be started with no filename if you'd prefer to start a new document and haven't decided on a name.

When you start vi there are a number of things you need to know to make it useful. The Return key has been included here because although some of these commands take effect immediately upon pressing the respective keys, others require Return to be pressed after them.

vi operates in one of two modes: command mode or insert mode. In command mode, you have control of things such as cursor position, deleting characters, and saving files. In insert mode, you can insert characters. This distinction is bound to be confusing at first, but you'll find that vi's speed and universal presence outweigh its odd interface when performing some tasks. Some of the most-used tasks are featured in Table 8.1.

TABLE 8.1 COMMON vi ACTIONS

| MODE | Key(s)/Key COMBINATION(s) | ACTION |
|---|---|---|
| Command | l | Move right |
|  | h | Move left |
|  | j | Move to the next line |
|  | k | Move to the previous line |
|  | Put cursor on the character to delete and then hit the x key | Delete a character |