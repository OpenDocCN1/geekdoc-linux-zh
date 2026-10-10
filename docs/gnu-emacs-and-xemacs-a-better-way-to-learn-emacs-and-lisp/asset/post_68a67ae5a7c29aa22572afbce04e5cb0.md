
## Chapter 16: Packages That Make Programming Easier

- A Mode for Nearly Every Language
- Dealing with Comments
- A Mode for C, C++, and Java
- JDE
- CPerl-mode
- Python Mode
- Searching in Multiple Source Files
- Emacs As an IDE

Emacs was originally a programmer's editor. The various language-specific modes have a long history of tuning and refinement. As new languages are developed, either an existing mode is adapted or an entirely new mode is written from scratch.

Aside from the language modes, many programmer's utilities are available. By choosing a set of these that fits your programming style, you can create a customized Emacs-based programming environment that can be as useful as one of the modern IDEs (*Integrated Development Environments*) common in the commercial software marketplace.

Source-code files are differentiated from one another as a convenience for the programmer. As far as the compiler is concerned, a directory of these files could be just one large file. In a project's source files, the units that matter more to the programmer are code blocks such as function and variable definitions, classes, and preprocessor conditionals. A statement in one file might refer to or invoke a definition in another file. Emacs provides several different methods of navigating through a directory of source files and locating a particular block of code. Tags, function menus, and the Speedbar window are three of these discussed later in this chapter.

### A Mode for Nearly Every Language

What makes a language mode useful to a programmer?

- Font locking helps visually separate different types of code and comments.
- Special keybindings allow rapid movement between statements or function definitions, analogous to text-mode's sentence and paragraph movement commands.
- Indentation can be automated and set to a particular style.
- Parentheses, brackets, and curly braces can be checked for balance.
- It has a built-in interface with compilers and debuggers.
- It can jump to the source files responsible for compiler-reported errors, one after another.

Not every language mode has all these features. In general, the more widely-used languages, such as C, C++, and Java, have the most powerful Emacs modes. Python and Perl, the two major interpreted languages, each have a mode that provides these features when appropriate.

### Dealing with Comments

Emacs provides several keyboard commands that ease the task of delimiting comments with comment characters and keeping your comments formatted nicely. These commands work for all major languages and many minor ones.

The M-q key command, used in text-mode to reformat paragraphs to a particular fill-column, has been modified in the programming modes so that it preserves indentation and discards excess comment characters that might not be needed after the operation. Pressing M-q while within this C comment block:

```
/* Here are some comments which could
 * be evened out and
 * formatted, just for appearance's sake
*/
```

results in this:

```
/* Here are some comments which could be evened out
 * and formatted, just for appearance's sake */
```

The indent-for-comment and comment-region commands can help you when you type comments. M-; moves point past the code and inserts opening and closing comment characters, leaving the cursor between them. The column that this command moves to is called the comment-column. By default, this is set to column 32. If your code is wider than 32 columns, you can use the set-comment-column command to set it to another value for the current buffer. Ctrl-x ; sets the current point position as the new comment-column. If you want it set permanently, you can use a line like this in your ~/.emacs file:

```
(setq comment-column 55)
```

As you type a comment to the right of a block of code, you might want your text to continue on a new line at the comment-column position rather than running off the right edge of the screen. Rather than pressing Enter for a new line, use the command M-j to indent for a new comment line. This key command also moves already-typed text down to a new indented line beneath the current line. If your comment looked like this, with point moved back between the words much and undo:

```
Fixnum undo-threshold;		/* Two thresholds controlling how much undo information to keep. */
Fixnum undo-high-threshold;
```

pressing M-j would format the comment lines like this:

```
Fixnum undo_threshold;    /* Two thresholds controlling how */
Fixnum undo_high_threshold; /* much undo information to keep. */
```

Sometimes it is easier to type in comment material while the ideas are fresh in your mind and not bother with comment characters until after you have finished. The comment-region key command, Ctrl-c Ctrl-c, surrounds a marked region with comment characters.

This can also be used on code you want to make “invisible” to the compiler, perhaps while diagnosing a malfunctioning source file. If you use the Ctrl-u Ctrl-c Ctrl-c command, the Emacs “universal argument,” it removes all comment characters from a selected region.

The next section introduces cc-mode, which evolved over the years from simpler C and C++ modes.

### A Mode for C, C++, and Java

cc-mode is a highly-evolved and well-maintained mode. It was developed from an earlier C mode by several people, including Barry Warsaw, coauthor of the Emacs Python mode. Currently, this mode is a team effort, with Martin Stjernholm acting as maintainer.

Unlike some other language modes, it has no provision for font locking, leaving those duties for font-lock mode itself. Some programmers don’t use syntax highlighting; cc-mode works equally well with or without it. The choice is up to the user.

If your source files have any of the conventional file name suffixes, such as .c, .h, .C, .cxx, .cpp, or .c++, cc-mode should start automatically when you view these files. You can see a complete list of recognized suffixes by using the Ctrl-h v (variable) help command. Requesting help on the auto-mode-alist variable causes a Help buffer to display a list of all suffixes that automatically call a particular mode.

If you use nonstandard file name suffixes, you can either start cc-mode manually (M-x cc-mode) or use a line such as this in your ~/.emacs file:

```
(add-to-list 'auto-mode-alist '("*.c\\|*.C\\|*.c+\\|*.c++" . cc-mode))
```

This makes cc-mode the default for any files ending in .cxt.

This mode’s power lies in two areas: syntactic navigation and maintaining a defined indentation style.

### Navigating through Source files

Words, sentences, and paragraphs might be logical units to move by in a text file, but cc-mode ignores these (except within comment blocks), providing keybindings that enable quick movement between expressions, functions, and lists:

- M-Ctrl-a Moves point to the beginning of a function.
- M-Ctrl-e Moves to the end of a function.

These two commands are extensions of M-a and M-e, which move point to the beginning or end of a sentence in text-mode. In cc-mode, these two key commands are used for movement within a statement:

- M-a Moves point to the beginning of a statement.
- M-e Moves to the end of a statement.

The next key commands enable quick movement through preprocessor conditional statements:

- Ctrl-c Ctrl-u Places point at the beginning of a preprocessor conditional.
- Ctrl-c Ctrl-p Moves to the previous preprocessor conditional.
- Ctrl-c Ctrl-n Moves point to the next preprocessor conditional.

The preprocessor conditional movement commands are particularly useful when you attempt to scan a source file in order to determine just which code is active under your platform. Conditional statements are heavily used in software that can be compiled for numerous operating systems, such as most GNU and open source software.

### Indentation Styles

Several distinct styles of indentation have evolved over the years for C and C++ source files. Rather strongly-held views on which style is more logical and readable have inspired many disputes, but it's really just a matter of taste and custom. cc-mode's default is a basic style from which the others are derived. The K&R style used in Kernighan and Ritchie's classic The C Programming Language is one of the choices offered, as is the GNU style, commonly used in many (but not all)
