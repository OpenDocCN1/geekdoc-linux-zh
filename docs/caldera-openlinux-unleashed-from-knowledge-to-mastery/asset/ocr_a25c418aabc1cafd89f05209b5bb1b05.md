| Mode | Description |
| --- | --- |
| font-lock-mode | This mode displays the text in different colors and fonts depending on the type of the text. You can also toggle this mode under the Syntax Highlighting menu item of the options menu. |
| auto-fill-mode | This mode enables automatic word wrapping. |
| overwrite-mode | This mode causes text to be overwritten instead of moved to the right when you type in new text. You can toggle this mode with the Insert button or from the options menu. |
| auto-save-mode | This option causes the buffer you are working on to be automatically saved periodically. This option is a must if you’re not in the habit of saving your work often. |
| line-number-mode | This mode causes the line number the cursor is on to be continuously displayed in the mode line. |
| blink-paren | When you place the cursor next to a parenthesis, brace, or bracket, this mode will cause XEmacs to make the matching parenthesis, brace, or bracket flash. This is very useful for determining the bounds of blocks of code in languages like C and practically a necessity for staying sane when editing languages like Lisp. (There is no “-mode” on this mode line.) |

# # Working with Multiple Windows

XEmacs will allow you to work in more than one window within a frame. We have already mentioned that you can open a file into a new window. You can also create new windows and close them whenever you want. Using windows, you can edit several files in a single frame, or you can edit at different locations within the same buffer. For example, you can create a second window and select the same buffer for each window. You can then view one area of a document while editing another. If the same area of the document is visible in both windows, you will see the changes you make in one window happen in the other window as well. Each window has its own mode line and echo area. Table 6.12 lists some commands for working with windows.

| Command | Description |
| --- | --- |
| Ctrl+X 0 (zero) | Close the selected window. If the current window is the only window in the frame, then the frame is closed as well, unless it is the only frame open. |