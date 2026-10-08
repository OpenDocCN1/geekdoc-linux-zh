# 290

# ed,

+   - 512 characters in a line.
- 256 characters in a global command list.
- 255 characters in the path name of a file (counting slashes).

The limit on the number of lines depends on the amount of user memory; each line takes one word. When reading a file, ed discards ASCII and null characters.

If a file is not terminated by a newline character, ed adds one and puts out a message explaining what it did.

/usr/bin/ed

If ed commands with arguments, it uses the default shell /usr/bin/sh (see sh(1)).

/usr/xpg4/bin/ed

/usr/xpg4/bin/ed is a POSIX-compliant version of the /usr/bin/ed command. See standards(5).

If ed executes commands with arguments, it uses /usr/xpg4/bin/sh, which is equivalent to /usr/bin/ksh (see ksh(1)).

# Regular Expressions

The ed command supports a limited form of regular expression. You can use regular expressions in addresses to specify lines and in some commands (com,s) to specify positions of a line that can be substituted. With ed addressing, at any time there is a current line. Generally, the current line is the last line affected by a command; the exact effect on the current line is discussed under the description of each command.

Internationalized Basic Regular Expressions are used for all system-localized locales. See regexp(5).

If the closing delimiter of an or of replacement string (for example, /) would be the last character before a newline, you can omit that delimiter, in which case the address is written. The following pairs are equivalent:

| s/s1 | s/s2 |
| g/s1 | g/s2 |
| ?s1 | ?s2 |

# ed Commands

Commands may require zero, or two addresses. Commands that require no addresses regard an address as an error. Commands that accept one or two addresses assume addresses when you specify an insufficient number of addresses; if you specify more addresses than such a command requires, ed uses the last one(s).

Typically, you separate addresses from each other by a comma (,) or a semicolon (;). If you use a semicolon separator, the first address is calculated, the current line (.) is set to that value, and then the second address is calculated. You can use this feature to determine the starting line for forward and backward searches. The second address of any two-address sequence must correspond to a buffer that follows the line corresponding to the first address.

In the list of ed commands, the parentheses shown before the command are not part of the address; instead, they show the default address(es) for the command.

You can precede an address by zero or more blank characters. You can precede the command by zero or more blank characters. If you use a suffix letter (l, n, or p), it must immediately follow the command