# CHANGING TEXT AND MOVING THROUGH YOUR DOCUMENT

To change text that's already in the file, you first need to reach it. You can move through your file in various ways. The arrow keys provide the simplest way, and they work just like you'd expect them to—they move you character by character through your file.

If you want to jump to the beginning or end of the current line, use the HOME and END keys, respectively. You can jump from word to word using ESC-F and ESC-B, or you can scroll page by page using CTRL-V (next page) and ESC-V (previous page). On some keyboards, the PGUP and PGDN keys work, too.

Text that you enter is inserted to the left of the cursor, and any text to the right of cursor is pushed to the right as you type. You can use the DEL key (or CTRL-D) to delete one character at a time, or press CTRL-K to delete all characters from the cursor to the end of the line.

# SEARCHING FOR TEXT

When you're working in a big file, you'll often want to locate a certain string of text. You can either scroll through the file until your eye catches it, or you can use CTRL-S to search using Emacs' less-than-elegant search tool.

As soon as you press CTRL-S, you can start to enter the text you want to find, but don't type too fast! As you enter your search string, Emacs immediately moves the cursor to a word in the file that matches what you've entered so far, so if you type too fast, you may miss something.

Try it. Starting at the top of the file, press CTRL-S and then type the letter b. The cursor should jump to the word bathtub right away. If you now type an r after the b, Emacs searches for br, and the cursor should jump to the word brightly. You can search backward, too, by using CTRL-R instead of CTRL-S.

# ADDING AND DELETING LINES

Let's practice adding and deleting lines now. To add a new line to your file, move the cursor to the end of a line (press END or use the right-arrow key), then press ENTER. A new blank line should appear after the current line. Pressing ENTER with the cursor at the beginning or end of a line adds a new blank line before the current line; pressing ENTER with the cursor anywhere else on a line splits the line at that point.

To delete a line, move to the beginning of the line (with the HOME key) and press CTRL-K. The line will become blank, but it will not go