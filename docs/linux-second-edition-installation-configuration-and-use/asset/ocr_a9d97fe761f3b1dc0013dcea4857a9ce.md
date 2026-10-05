# EMACS PROGRAMMING SAMPLES 581

[delete] or [deletechar] or [DEL]
[backspace] or [DEL]
[insert] or [insertchar]
[F1] to [F12]

# 17.5 Emacs programming samples
Exchanging two letters

With the key combination C-T you can exchange the letter at the cursor position with the preceding letter. In principle, it is OK - apart from the fact that, during many years of working with a different text editor, I have been used to exchange the letter at the cursor position with the next letter - and not with C-T, but with F1. To make Emacs behave in the same way, and not the following easily understandable macro has been introduced:

```
(defun swap-char()
 ;exchange two letters at cursor position
  (interactive)
  (save-excursion)
   (forward-char)
   (transpose-chars 1)))
  (global-set-key [F1] 'swap-char) ;F1 under X
```

The function save-excursion saves the cursor position. The cur-sor is moved one character forward with forward-char and the built-in transpose-chars is called to exchange the last two letters. With global-set-key, the new function is assigned to the F1 key.

# Automatic loading and saving of abbreviations

On page 564, we have described how you can define abbreviations. Such definitions are, however, not loaded or saved automatically when you start or exit Emacs. And this is exactly what the following three lines in .emacs provide:

```
(setq-default abbr-mode t) ;automatically activate abbr-mode
(read-abbrev-file "/.emacs-abbrev") ;load abbrev file "/.emacs-abbrev"
(setq save-abbrevs t) ;automatically save when changed
```

set-default assigns a default value to, where the assignment of t corresponds to the truth value true of other programming languages.

Opinions about automatic expansion of abbreviations differ. It can be rather irritating when Emacs suddenly recognizes some unwanted character combinations as abbreviations. If you prefer to expand your abbreviations manually, you can remove