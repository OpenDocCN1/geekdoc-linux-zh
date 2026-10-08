# Chapter 12: Working with Texts

+   - l or right-arrow: Move the cursor forward one character in the current line.
- j or down-arrow: Move the cursor down one line, maintaining the current column position in the new line when possible.
- k or up-arrow: Move the cursor up one line, maintaining the current column position in the new line when possible.

Cursor movement commands as h, j, k, and l may initially seem pretty strange or at least counterintuitive, remember that vi was originally designed to be used on terminals, some of which didn't have the arrow keys. Ask your grandfather.

# Note

When in Insert mode, the old-time vi movement commands (h, j, k, and l) insert those letters rather than moving the cursor (vi is a modal editor, remember?). However, the arrow cursor movements "do the right thing" when you're in Insert mode — they simply move the cursor but leave you in Insert mode.

As mentioned previously, you can repeat these simple cursor movement commands any number of times by prefixing them with a numeric argument. For example, you can move the cursor forward five lines by typing 5l, up five lines by typing 5k, and so on. This is handy, but requires you to count how far you want to move the cursor first. That seems somewhat tedious when you really want to do things like move to the next word, move to the previous word, or (commonly) go to some local place in the current file. To simplify things, it provides handy cursor movement commands like the following:

+   - b: Move backward one word.
- w: Move forward one word.
- ^: Move to the beginning of the current line.
- $: Move to the end of the current line.
- (: Move to the beginning of the current sentence.
- ): Move to the end of the current sentence.
- [: Move to the beginning of the current paragraph.
- ]: Move to the end of the current paragraph.
- 1G: Go to the first line in the current file.
- 0G: Go to the last line of the current file. Just pressing G in vim does the same thing, but may not work in all versions of vi.

The last two commands are actually examples of the standard vi commands to go to a specific line, and they highlight how nicely vi commands work with numeric arguments. For example, you could move to the 14th line in your file by typing the 14G command. Similarly, you could move to the end of the third paragraph from your current position by typing 3) command.

433