One after another, carriage returns (which look like `^M` on a Linux system) are found and then passed to `replace-match`, which substitutes nothing in their place. Remember that the `while` function is in charge of this operation. After `search-forward` has found the last carriage-return symbol and passed it to `replace-match`, `while` stops and returns the `nil` value to the Lisp interpreter. The interpreter sees that `while` has finished, and it moves on to the last line in the main function.

If the fourth and fifth lines were translated into an English command, they might look something like this:

> Starting at the beginning of the buffer, look for carriage returns, and delete them. When you can’t find any more, stop.

The last line of `dos-unix` is optional. The `message` built-in function is used to display a string of text to the user. In `dos-unix`, `message` is called with a string, “`Operation complete`”, as an argument. When `dos-unix` has finished its work, that string is shown in the minibuffer.

# ## dos-unix As a Template

The `dos-unix` function can be easily changed by simply substituting other strings for `\r\*` and `**` in the arguments given to `search-forward` and `replace-match`. Try opening a text file in one window and the `dos-unix` function in another. Change the strings in `dos-unix`, reevaluate the function, and then run it on the text file. Such experimentation is a good way to become familiar with how functions work.

Remember that all the built-in functions used in `dos-unix` have their own internal documentation. Use the `Ctrl-h f` help key to learn more about them.

# ## Variables

A Lisp variable is like a variable in other programming languages. A variable is just a name used to refer to some sort of value, which may be a number or a Lisp expression. Variables can be defined using the built-in function `defvar` (an abbreviation of “define variable”). A variable can be global, affecting all Lisp procedures used by Emacs; or it may be local, in which case it is effective only in the function in which the variable was defined or set.