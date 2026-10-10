# Manipulating Text in Command Mode

The first method you need to know in order to manipulate text is how to move around in the vi editor. Table 10.1 provides a list and corresponding descriptions of typical methods for moving your cursor in vi while in Command mode. There are even more maneuvering commands available than those listed in Table 10.1, too. Check vi's man pages or other information sources for further help.

# Deleting Text

There are many commands available for deleting text in Command mode. We list several ways of doing so in Table 10.2 along with two commands to use if you want to undo the deletion. For additional commands, check Appendix A as well as the man pages and other information sources.

# Searching for Text Strings

When you are in Command mode, pressing the forward slash ( / ) button automatically puts you in text search forward mode and takes you to the last line on the screen, where vi has placed a forward slash prompt. Similarly, pressing the question mark ( ? ) automatically puts you in text search backward mode and takes you to the last line on the screen, where vi has placed a question mark prompt.

After the prompt, enter the string of text you want to search for and press Enter. The search begins in the chosen direction from the position of the cursor. The cursor stops underneath the first character of the first found text string. If you want to continue searching in the same direction, press n. If you want to search in the opposite direction, press N. Eventually, you will reach the bottom or top of the file, and vi will notify you when you do.

To exit from text search, simply enter any other command. You do not press Esc first.

# Searching for and Replacing Text

Manually cutting and pasting can be tiresome, inefficient, and occasionally inaccurate. The following is a command for automating it when you are in Command mode in vi: