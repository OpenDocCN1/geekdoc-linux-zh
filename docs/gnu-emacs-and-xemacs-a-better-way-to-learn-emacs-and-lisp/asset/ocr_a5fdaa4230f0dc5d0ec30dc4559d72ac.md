pressing M-j would format the comment lines like this:

```
Fixnum undo_threshold;    /* Two thresholds controlling how */
Fixnum undo_high_threshold; /* much undo information to keep. */
```

Sometimes it is easier to type in comment material while the ideas are fresh in your mind and not bother with comment characters until after you have finished. The comment-region key command, Ctrl-c Ctrl-c, surrounds a marked region with comment characters.

This can also be used on code you want to make “invisible” to the compiler, perhaps while diagnosing a malfunctioning source file. If you use the Ctrl-u Ctrl-c Ctrl-c command, the Emacs “universal argument,” it removes all comment characters from a selected region.

The next section introduces cc-mode, which evolved over the years from simpler C and C++ modes.

# A Mode for C, C++, and Java

cc-mode is a highly-evolved and well-maintained mode. It was developed from an earlier C mode by several people, including Barry Warsaw, coauthor of the Emacs Python mode. Currently, this mode is a team effort, with Martin Stjernholm acting as maintainer.

Unlike some other language modes, it has no provision for font locking, leaving those duties for font-lock mode itself. Some programmers don’t use syntax highlighting; cc-mode works equally well with or without it. The choice is up to the user.

If your source files have any of the conventional file name suffixes, such as .c, .h, .C, .cxx, .cpp, or .c++, cc-mode should start automatically when you view these files. You can see a complete list of recognized suffixes by using the Ctrl-h v (variable) help command. Requesting help on the auto-mode-alist variable causes a Help buffer to display a list of all suffixes that automatically call a particular mode.

If you use nonstandard file name suffixes, you can either start cc-mode manually (M-x cc-mode) or use a line such as this in your ~/.emacs file:

```
(add-to-list 'auto-mode-alist '("*.c\\|*.C\\|*.c+\\|*.c++" . cc-mode))
```

This makes cc-mode the default for any files ending in .cxt.

This mode’s power lies in two areas: syntactic navigation and maintaining a defined indentation style.