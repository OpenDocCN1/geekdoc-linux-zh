Emacs was originally a programmer's editor. The various language-specific modes have a long history of tuning and refinement. As new languages are developed, either an existing mode is adapted or an entirely new mode is written from scratch.

Aside from the language modes, many programmer's utilities are available. By choosing a set of these that fits your programming style, you can create a customized Emacs-based programming environment that can be as useful as one of the modern IDEs (*Integrated Development Environments*) common in the commercial software marketplace.

Source-code files are differentiated from one another as a convenience for the programmer. As far as the compiler is concerned, a directory of these files could be just one large file. In a project's source files, the units that matter more to the programmer are code blocks such as function and variable definitions, classes, and preprocessor conditionals. A statement in one file might refer to or invoke a definition in another file. Emacs provides several different methods of navigating through a directory of source files and locating a particular block of code. Tags, function menus, and the Speedbar window are three of these discussed later in this chapter.

# ## A Mode for Nearly Every Language

What makes a language mode useful to a programmer?

+   - Font locking helps visually separate different types of code and comments.
+   - Special keybindings allow rapid movement between statements or function definitions, analogous to text-mode's sentence and paragraph movement commands.
+   - Indentation can be automated and set to a particular style.
+   - Parentheses, brackets, and curly braces can be checked for balance.
+   - It has a built-in interface with compilers and debuggers.
+   - It can jump to the source files responsible for compiler-reported errors, one after another.

Not every language mode has all these features. In general, the more widely-used languages, such as C, C++, and Java, have the most powerful Emacs modes. Python and Perl, the two major interpreted languages, each have a mode that provides these features when appropriate.