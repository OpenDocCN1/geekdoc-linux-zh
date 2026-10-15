# Example 2-23 Inserting three duplicate lines

```
=3== I want three more copies of this line.
==== They will appear before this line.
```

When you press Enter, the file displays output similar to Example 2-24.

# Example 2-24 Output from inserting three duplicate lines

```
==== I want three more copies of this line.
==== I want three more copies of this line.
==== I want three more copies of this line.
==== I want three more copies of this line.
==== They will appear before this line.
```

To duplicate a block of lines, either one time or a specified number of times, type two double quotation marks (") in the first and last lines of the block. A number can precede or follow the first double quotations (for example, 5") to duplicate the block more than one time.

When you type one double quotation mark (") and press Enter, the status area of the screen displays the following status, allowing you to scroll the window before completing the block and pressing Enter:

```
"" pending...
```

> z/OS analogy: In z/OS, this is similar to using the R n (repeat) line command in ISPF editor.

# Moving lines

To move one line, enter the single character M (move) in the prefix area of the line to move. Indicate its destination by entering either the character F (following) or P (preceding) in the prefix area of another line. After you press Enter, the line containing the M is removed from its original location and is inserted in either immediately following the line containing the F, or immediately preceding the line containing the P, as appropriate.

A number can precede or follow the M to indicate moving more than one line (for example, 5M or M5) in the prefix area. The line to move and the destination line can be on different screens.

After you enter M, F, or P, the status area of the screen displays a Pending status. This pending status allows you to scroll the screen before entering the other prefix subcommand.