# Is there something I can do if I don’t like the word I just entered?

Yes; press CTRL-W to retype it. This is one of the few ways you can move the cursor position while staying in insertion mode.

# What if I want to start my text insertion all over?

Press CTRL-U. The other way to do this is to ESC back to command mode and press u for undo. The undo command is only a single level deep, though, so undo immediately, or you will have to fix it the hard way.

# How can I undo all the changes I’ve made to the current line?

Try pressing U from command mode. This gets around the single-level undo limitation, but only for the current line. Once you move your cursor off the line, you can’t undo the changes on that line, unless they’re still in the single-level undo buffer.

# Can I replace the current character and then insert more text without overwriting what’s there?

Yes; use the s command. We know we can replace a single character with r, and we can insert text with i or a, but by using s we get around the limitations of r without having to worry about overwriting something we don’t want to. If you want to replace the next ten characters, and then start inserting text, just type 10s and start making your change.

# How about replacing the entire current line?

Use S. This will delete the current line, move the cursor to the first column, and change to insert mode.