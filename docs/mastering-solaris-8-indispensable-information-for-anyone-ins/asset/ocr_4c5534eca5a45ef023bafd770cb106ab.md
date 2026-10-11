It is worth noting that vi specifies a word as a sequence of characters without spaces, punctuation (., " ?-), or digits. Therefore, 9 is the first word and th is the second. Similarly, 99? would be two words: 99 and ?. vi makes provisions for the standard space-delimited words by providing the navigation commands W, B, and E.

A line is a string of characters separated by the newline character or by a return. Paragraphs are considered to be lines separated by one or more blank lines on each side.

Although you don’t see line numbers in vi unless you specify that you want to see them, the program keeps track of the number of lines in your text file. You can use the ng keystroke to jump to the line numbered n. To see the line numbers in your display, use the :set nu command (which stands for “set number of”). You turn off numbering by issuing the :set nonu command.

One rarely used feature of vi is the use of markers to mark positions in your file. Markers exist only during a session, but they serve the same role as bookmarks, providing a position in the file you can jump to during your work. To set a marker, move to the start of the line you wish to mark and give the ma command. This creates the a marker for that line. Unless you delete the line or specify the marker again at a different line beginning, the a marker stays with that line.

Markers serve as positions that you can use in ranges with other commands. For example, use the d’a command to delete everything from the cursor’s current position to the beginning of the a marker line.

# ## Editing in the vi Editor

The most commonly used editing commands are those that put you into the Input submodes. These are i (insert before the current character) and a (append text right after the cursor position). You can also use the I and A commands to enter text at the beginning of the current line or enter text at the end of the line, respectively. I and A save you from having to reposition the cursor prior to text entry.

As you are entering text, you can correct the mistakes you make by using the same commands that you would at the shell, including the Erase (Ctrl+H), Line Kill (Ctrl+U), and Word Kill (Ctrl+W) keystrokes. As you move the cursor backward in the Insert mode, vi doesn’t remove text. However, as you enter new text or press Return, the old text is moved down the document to make room for the new text.

Two other common commands are the o and O commands, which are used to create open lines. The o command opens a new line directly below the current line, and