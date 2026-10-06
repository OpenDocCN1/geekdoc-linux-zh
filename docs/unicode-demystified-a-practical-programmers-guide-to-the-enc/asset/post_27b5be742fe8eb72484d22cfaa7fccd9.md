
# Basic Editing Commands 48

Pressing DELETE removes characters to the left of the cursor. The cursor and the remainder of the text on this line move to the left each time you press DELETE. To join a line with the line above it, position the cursor on the first character of the second line and press DELETE.

Press CONTROL-D to delete the character under the cursor. The cursor remains stationary, and the remainder of the text on this line moves left to replace the deleted character. See the tip “More about Deleting Characters” on page 477 if either of these keys does not work as described.

# Saving and Retrieving the Buffer

No matter what happens to a buffer during an emacs session, the associated file is not changed until you save the buffer. If you leave emacs without saving (this is possible if you are inconsistent enough), the file is not changed, and the session's work is discarded.

As mentioned previously, emacs prompts for unsaved changes to the buffer contents. As it writes a buffer’s edited back to the file, emacs may optionally first make a backup of the original file contents. You can choose among no backups, one level (default), or an arbitrary number of levels. The one-level backup filenames are formed by appending the ~-n to the original filename where n is the sequential backup number, starting with 1.

The command CONTROL-X CONTROL-S saves the current buffer in its associated file. The emacs editor confirms a successful save with a message in the Echo Area.

If you are already editing a file with emacs and wish to begin editing another file (also called visiting a file), you can copy the new file into a new emacs buffer by giving the command CONTROL-X CONTROL-F. The emacs editor prompts you for a filename, that reads that file into a new buffer, and displays that buffer in the current window. Having two files open in one session is more convenient than exiting emacs, returning to the shell, and then starting a new copy of emacs to edit a second file.

# Basic Editing Commands

This section takes a more detailed look at the fundamental emacs editing commands. It covers straightforward editing of a single file in a single window.

482 Chapter 11 The emacs Editor

# Visiting a File with CONTROL-X CONTROL-F

When using CONTROL-X CONTROL-F, emacs partially completes the path to the filename you are to enter. Normally this is the path to the working directory, but in some situations emacs may display a different path, such as the path to your home directory. You can edit this already displayed path if it is not pointing to the directory you want.

# Keys: Notation and Use

Mainstream emacs uses 128-character ASCII codes. ASCII keyboards have a typewriter-style SHIFT key and a CONTROL key. Some keyboards also have a META (diamond or ALT) key that controls the eighth bit. It takes seven bits to describe an ASCII character; the eighth bit of an eight-bit byte can be used to communicate other information. Because so much of the emacs command set is in-printing CONTROL or META case, Stallman was one of the first to confront the developing a notation for writing keystrokes.

Its solution, although not popular outside the emacs community, is clear and unambiguous (see Table 11-1). It uses the capital letters C and M to denote holding down the CONTROL and META keys, respectively, and a few simple acronyms for the most special characters, such as RET (this book uses RETURN), LFD (LINEFEED), DEL (DELETE), ESC (ESCAPE), SPC (SPACE), and TAB. Most emacs documentation, including the online help, uses this notation.

| Character | Classic emacs Notation |
| :--- | :--- |
| (lowercase) a | a |
| (uppercase) A | A |
| CONTROL-a | C-a |
| CONTROL-A | C-A (do not use SHIFT), equivalent to CONTROL-a |
| META-a | M-a |
| META-A | M-A (do use SHIFT) |
| CONTROL-META-a | C-M |
| META-CONTROL-a | M-C (not used frequently) |

483 Basic Editing Commands

This use of keys had some problems. Many keyboards had no META key, and some operating systems discarded the META bit. Emacs clashes with XON-OFF flow control, which also uses CONTROL-S and CONTROL-O and continues to do so today. The flow control still exists, the META key was resolved by making it an optional two-key sequence with ESC. For instance, you can type ESC-a in place of META-a or ESC-CONTROL to get CONTROL-a. If your keyboard does not have META or ALT key, you can use the two-key sequence by pressing ESC key, releasing it, and then pressing META key. For example, when this book says press META-r you can either press META or ALT key while pressing ESC and press r.

An aside on notation: This book uses uppercase letter following CONTROL key and a lowercase letter following META key. In either case not ever have to hold down SHIFT key while entering CONTROL or META character. The uppercase character (that is, META-A) is a different character, it is usually set up to cause no action or same effect as its lowercase counterpart.

# Key Sequences and Commands

The relationship between key sequences (one or more keys that are pressed together or in sequence to issue an emacs command) and commands is very flexible, and there is considerable opportunity for exercising your personal preference. You can translate and remap key sequences to other commands or replace commands themselves. Most emacs documentation glosses over all the details and talks about keystrokes as though they were the commands, is important to know that the underlying machinery is separate from the key sequences and to understand that the behavior of the key sequences and the commands can be changed (page 515).

# META-x: Running a Command without a Key Binding

The emacs keymaps (the tables, or vectors, that emacs uses to translate sequences to commands [page 517]) are crowded, and often it is not possible to bind every single command to a key sequence. You can execute any command by name by preceding it with META-x. The emacs editor prompts you for a command in the Echo Area and executes the command after you enter the command name and press the return key.

Sometimes, when a command has no key sequence, it is described as META-x command-name. The emacs editor has smart completion for answers, using SPACE or TAB to complete, if possible, to the end of the current word or the whole command, respectively. Forcing a completion past the last unambiguous point or typing ? displays a list of alternatives. .

# Numeric Arguments

Some of the emacs editing commands take a numeric argument and interpret it as a repetition count. The argument immediately prefixes the key sequence for the command, and the most common case of no argument is almost always interpreted as a count of 1. Even an ordinary alphabetic character can have a numeric argument, which means "insert this many times." To give a command numeric argument, you can do either of the following:

- Press META with each digit (0–9) or the minus sign (-) (for example, to insert 10 characters, type META-10).
- Use CONTROL-U to begin a string of digits, including the minus sign (for example, to move the cursor forward 20 words, type CONTROL-U 20).

For convenience CONTROL-U defaults to multiply by 4 when you do not follow it with a string of one or more digits. For example, entering CONTROL-U r means insert rrrr (4 × 1), whereas CONTROL-U U means insert rrrrrrrr (4 × 4). For quick partial scrolling of a tall window, you might find it convenient to use repeated sequences of CONTROL-U CONTROL-V to scroll down four lines, CONTROL-U META-V to scroll up four lines, CONTROL-U CONTROL-U CONTROL-V to scroll down 16 lines, or CONTROL-U CONTROL-U META-V to scroll up 16 lines.

# Point and the Cursor

Point is the place in a buffer where editing takes place, and this is where the cursor is positioned. Strictly speaking, Point is the left edge of the cursor—it is thought of as always lying between two characters.

Each window has its own Point, but there is only one cursor. When the cursor is in a window, moving the cursor also moves Point. Switching the cursor out of a window does not change window’s Point; it is in the same place when switching the cursor back to that window.

All the cursor-movement commands previously described also move Point. In addition, you can move the cursor to the beginning of the buffer with META-< or to the end of the buffer with META->.
