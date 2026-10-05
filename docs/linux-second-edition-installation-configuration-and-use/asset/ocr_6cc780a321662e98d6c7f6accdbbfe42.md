# 560 EMACS - KING OF ALL EDITORS

Two changes in the behavior of Emacs concern special characters: now, instead of the " character, Emacs inserts `` or '', that is, a pair of single quotes. A "character can only be entered directly after a backslash (\). (Page 584 describes how this irritating feature can be switched off.)

At the input of every second S, the cursor briefly jumps back to the preceding S to show where the mathematical formula started. (Under TeX and LaTeX, S...S has the function of a pair of brackets which encloses commands for the definition of a mathematical formula.) Furthermore, Emacs now provides some additional aids:

# LaTeX mode

```
Ctrl+C, Ctrl+E creates the instruction \end(name) for the last
open command \begin(name)
Ctrl+C, Ctrl+O name creates the instruction \begin(name),
empty line, \end(name)
Ctrl+C, J jumps to the closing bracket of the
current level of parentheses
Ctrl+J terminates a paragraph, inserts an additional
empty line and carries out a syntax check on the
paragraph (missing, and so on)
```

Both modes have defined commands for calling TeX or LaTeX. These commands, however, only make sense when the whole document is contained in a single file. Under Linux, it is usually more practical to start TeX or LaTeX from a separate console or a shell window.

The Alt+X validate-text-buffer command is much more attractive; this searches the current text for TeX or LaTeX syntax errors. Even though the LaTeX command sometimes signals errors which are not (especially when the LaTeX command |verb or the LaTeX environment verbatim is used), it has certainly helped me to find many missing (< or ) brackets.

For professional LaTeX/Emacs users, the AUC TeX package provides a considerable enhancement of LaTeX: the AUC TeX package defines many additional Emacs macros. One of the most attractive features is that after a translation you can advance to the next error with a simple click of the mouse. AUC TeX is integrated into more recent Emacs versions; for older GNU versions, it must be installed separately. Subsequently, you must insert the line (require 'tex-site') into .emacs. With this range of additional AUC TeX commands is automatically available in LaTeX mode. Documentation on AUC TeX can be found in the framework of the Emacs Info documentation and in the file auc-tex.dvi.

![](bbox=[0.235, 0.705, 0.263, 0.803])