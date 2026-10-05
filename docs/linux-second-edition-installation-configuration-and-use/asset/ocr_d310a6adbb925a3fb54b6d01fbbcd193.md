If you cannot get used to area selection with Ctrl+X GNU Emacs allows you to use the usual Windows form of selection with Shift. To activate this feature, simply execute Alt+X pc-selection. If you want to use this form as a default setting, you will need to insert the following lines into .emacs:

```
(custom-set-variables
```

```
'(pc-selection-mode t nil (pc-select)))
```

Unfortunately, there is no corresponding mode for XEmacs.

# Intermediate storage of texts in registers

As can be seen from the above paragraphs, Emacs has a standard buffer in which the most recently deleted text is stored so that it can subsequently be inserted with Ctrl+Y. Furthermore, Ctrl+X U can be used to carry out a multi-level undo. In addition, Emacs offers the possibility of intermediate text storage in registers. These registers, which are identified by a letter or a digit, can be inserted into a text any number of times. Registers are particularly useful when you frequently need similar formulations or keywords within a text. Registers (and the deletion buffer) are not saved when Emacs is terminated! If you define the same registers, you should think about defining macros or abbreviations instead which can also be saved (see page 565 and following).

# Text registers

+   - Ctrl+Spacebar sets an invisible marking point stores the text between the current cursor position and the marking point in the char register (register save)

+   - Ctrl+X, R, S char inserts the contents of the char register (register insert)

# 16.6 Elementary editing commands

# Inserting and overwriting of text

Usually, Emacs is in insert mode, that the newly entered text is inserted into the existing text at the cursor position. If you want to overwrite the existing text instead, you must use Alt+X overwrite-mode switch to overwrite mode. A repeated execution of the command switches back to insert mode. With a correct keyboard configuration, you can also simply use Ins to toggle between modes.