# Rectangles and Registers

Ctrl-x r k Kills the rectangle formed by positioning point and the mark diagonally from each other.

Ctrl-x r x Copies a rectangular region to a named register.

Ctrl-x r y Pastes the most recently killed rectangular region.

Ctrl-x r t Inserts a text string to the left of each line in a rectangle.

Ctrl-x r c Removes all characters from a rectangle and leaves spaces in their place.

Ctrl-x x Spacebar x Saves the current point position in a register named x. You can have many of these saved positions at once, each with its own name. The name can be a word or a single character.

Ctrl-x x j x Jumps to the point position saved in register x.

Ctrl-x x a x Copies the selected region into a register named x.

Ctrl-x x r x Inserts the contents of register x into the current buffer. This can be a normal or rectangular register.

# Bookmarks

See also the bookmarking minibuffer commands in Appendix B.

Ctrl-x x m Sets a bookmark in the current buffer at point.

Ctrl-x x m xxx Sets a bookmark named xxx at point.

Ctrl-x x b xxx Jumps to a bookmark named xxx and loads the file if necessary.

Ctrl-x x l Opens a buffer containing a list of all bookmarks.

# Abbreviations

See also the abbreviation commands in Appendix B.

Ctrl-x a g Defines an abbreviation.

Ctrl-x a l Defines an abbreviation for the current major mode only.

Ctrl-x a i g Defines the word at point as an abbreviation.