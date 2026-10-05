A different syntax applies for setting colors in info mode. The following lines have been created with the aid of [Alt]+X customize-browse.

```
(custom-set-faces
(info-xref (t :bold t :foreground "blue\))
(info-node (t :bold t :italic :foreground "red\))))
```

# Modifying a processing mode

If you want to change Emacs' behavior, not globally, but only for a processing mode, you must work with mode-hook variables. The code stored in these variables is automatically executed as soon as the processing mode is activated. add-hook appends a new function to the existing contents of a hook variablenThe following lines modify the TeX mode of Emacs; every time the TeX mode is activated. auto-fill-mode activates flow text mode as well. To prevent breaking in this mode in the 70th column (the fill-column variable is set to 79). The final modification regarding inputting the " character: in TeX mode. Emacs has the unpleasant habit of changing this character to ' and ''. To prevent this, the variables tex-open-quote and tex-close-quote are both assigned the character " (code 34).

Finally, we need to explain the keyword Lambda: similarly to define, in its structure defines a difference. A difference allows in the fact that the function does not have to be named. In addition, the preceding quote ' causes the following lines not to be evaluated but to be stored as code.

```
add-hook 'tex-mode-hook      ;settings for Tex mode
(function (lambda ()
(auto-fill-mode)               ;flow text mode
(set fill-column 79)          ;full width
(set tex-open-quote 34)
(set tex-close-quote 34)      ;no fuss with"
(and window-system)
(progn
(font-lock-mode 1)         color representation
(set-face-foreground)      'font-lock-comment-face "blue"
(set-face-foreground)      'font-lock-string-face "red"
(set-face-foreground)      'font-lock-keyword-face "magenta"
)))
```

# Percentage cursor movement in large texts

Emacs shows in the status line at which percentage range of the text you currently are (thus, about 50 per cent for the middle position). Unfortunately, the text mode lacks a command which allows you to move the cursor quickly to a position that is expressed as a percentage value (When using Emacs under X, you will not miss this