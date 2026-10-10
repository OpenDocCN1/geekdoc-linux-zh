The only difference between the old version is the addition of this line:

```
(save-excursion
```

and an additional parenthesis at the end, which is needed to close the one at the beginning of the new `save-excursion` line. The two new parentheses effectively enclose the body of the function; now the entire operation of `dos-unix` is subsidiary to the `save-excursion` function.

To help make it easier to experiment with the `dos-unix` function (you might not have any DOS-format files handy to test with), here is an opposite function called `unix-dos`:

```
  (defun unix-dos ()
    "*Insert DOS carriage-return characters into a buffer.*
    (interactive)
    (save-excursion
    (goto-char (point-min))
    (while (search-forward "\n" nil t) (replace-match "\r\n"))
    (message "Operation complete")))
```

In this function, `search-forward` is looking for newline characters rather than carriage returns. `"\n"` is the slash-escaped symbol for the invisible newline character, just as `"\r"` is the symbol for the carriage-return character (which is invisible on a DOS-based system but is visible when viewed under Linux). When you run `unix-dos`, every newline character is replaced with both a newline and a carriage return.

Try both the old version of `dos-unix` and the new, and you will see the difference that `save-excursion` makes.

# # How Parentheses Are Used

By now you probably have noticed how parentheses are used in a Lisp statement. Emacs looks for parentheses in a function or another Lisp statement and relies on them to separate one list from another.

Notice how in the sample function `unix-dos` each separate function operation is enclosed in parentheses. The entire `dos-unix` function is itself surrounded by parentheses. Here’s a simple rule of thumb: Each time a new function is introduced, contain it within its own parenthesized expression.