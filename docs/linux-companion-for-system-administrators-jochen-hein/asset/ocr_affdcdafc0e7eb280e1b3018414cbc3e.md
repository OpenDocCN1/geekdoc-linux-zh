# CONFIGURATION 161

If a function does not exactly do what you want, you can redefine it at runtime and interactively as desired. That makes it easy to customize Emacs.

# 5.3.1 Configuration files

When Emacs is loaded, the file ~/.emacs is read first. This file contains Emacs Lisp commands that can be used to modify the appearance or behaviour of Emacs. In this file, users can configure the editor to suit their preferences. Subsequently, if the variable inhibit-default-init is not nil, the file default.el is loaded.

In addition, there may be a system-wide file (init.el) which is loaded before ~/.emacs. Loading this file can be prevented with the command line option -no-site-file. However, this should only be necessary in rare cases, for example, for error detection purposes.

Each of these files contains Lisp code. As a rule, you need not be a Lisp expert, for many applications, appropriate suggestions for configuration can be found in the (X)Emacs FAQ, in the info system or in the Lisp files of the corresponding modes. Whatever else you need to know about Lisp will be shown in the following sections.

The name Lisp is an abbreviation of 'List programming.' Lists (please note: programs or Lisp functions are not including lists, too) are enclosed in parentheses. Therefore it quite often happens that several closing parentheses appear at the end of a line or function (this is the origin for the expansion 'Lots of Insertion Superfluous Parentheses' for LISP). When inserting a new opening parenthesis is highlighted in lisp-mode. This is of great help for the programmer or user. The Emacs FAQ contains more hints and tips on this subject.

Comments in Lisp begin with a semicolon (;) and end with the line end. The Lisp mode of Emacs (not the Lisp interpreter) differentiates between comments that begin with one, two, or three semicolons. These mark comments which are to be indented at different levels. One semicolon means to indent to column 40, two stand for the same indent as the current code and comments, and comments starting with three semicolons stay exactly where they were. By using the Tab key (lisp-indent-line), a line can be formatted accordingly.

Emacs provides some functions which make Lisp programming almost a pleasure. Highlighting corresponding pairs of parentheses is only one example. You can process a configuration file without leaving Emacs by using the eval-buffer command. You can pass a region to the Lisp interpreter with eval-region. These functions are available in elisp-mode and in the