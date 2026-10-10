# **Navigating through Source files**

Words, sentences, and paragraphs might be logical units to move by in a text file, but cc-mode ignores these (except within comment blocks), providing keybindings that enable quick movement between expressions, functions, and lists:

M-Ctrl-a	Moves point to the beginning of a function.
M-Ctrl-e	Moves to the end of a function.

These two commands are extensions of M-a and M-e, which move point to the beginning or end of a sentence in text-mode. In cc-mode, these two key commands are used for movement within a statement:

M-a	Moves point to the beginning of a statement.
M-e	Moves to the end of a statement.

The next key commands enable quick movement through preprocessor conditional statements:

Ctrl-c Ctrl-u	Places point at the beginning of a preprocessor conditional.
Ctrl-c Ctrl-p	Moves to the previous preprocessor conditional.
Ctrl-c Ctrl-n	Moves point to the next preprocessor conditional.

The preprocessor conditional movement commands are particularly useful when you attempt to scan a source file in order to determine just which code is active under your platform. Conditional statements are heavily used in software that can be compiled for numerous operating systems, such as most GNU and open source software.

# **Indentation Styles**

Several distinct styles of indentation have evolved over the years for C and C++ source files. Rather strongly-held views on which style is more logical and readable have inspired many disputes, but it's really just a matter of taste and custom. cc-mode's default is a basic style from which the others are derived. The K&R style used in Kernighan and Ritchie's classic The C Programming Language is one of the choices offered, as is the GNU style, commonly used in many (but not all)