# # The vi Editor

The vi(1) command is a screen-oriented text editor. The following sections cover the three modes of operation, controlling the cursor position, manipulating text (add, delete, copy, and move), and search/replace functions.

![](bbox=[0.12, 0.219, 0.224, 0.285])

In this description of the vi text editor, I use the symbols < and > to define a key you should press on the keyboard. For example, <a> indicates that you should press the key labeled “a,” and <Enter> indicates that you should press the key labeled “Enter” or “Return.”

# ## Modes of Operation

The vi editor has three modes of operation:

+   - Command
+   - Input
+   - Last Line

Command mode is the initial and default mode of operation. In this mode, file navigation is supported so that you can view different parts of the file. You control the view by using commands to scroll the file forward or backward (vertically on the screen) and to move between the left and right side of the display. Character, word, and line deletion is also supported in Command mode.

Input mode allows text to be added, deleted or modified. This mode provides a variety of commands to manipulate a file’s text contents.

Last Line mode supports the input of commands to save changes, perform searches, and execute other ex(1) and ed(1) commands.

# ## Command Mode

The main functions of Command mode are navigation and deletion. Navigation enables you to position the cursor at a certain location within the file. You can then perform deletion or Input mode operations (add or modify) on the file contents.

# ### Cursor Positioning

Table 10.2 lists the commonly used cursor-positioning keyboard sequences. See the vi(1) manual page for additional commands.