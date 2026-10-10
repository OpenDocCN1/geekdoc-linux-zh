statement. Remember that the Lisp interpreter assumes that the first symbol in a statement refers to a function.

Symbol names are arbitrary, but Lisp programmers attempt to give them some sort of mnemonic value, just for code clarity. A symbol can't have any white space, because Emacs would try to interpret it as two symbols.

Using the same symbol to refer to more than one function or variable will cause unpredictable results. Another possible source of problems is redefining an existing Lisp function; you're better off defining an entirely new function.

# True and False Values

Many Lisp expressions can have a value of either true or false—t or nil in Lisp terminology. Here's an example:

```
(setq initial-scratch-message nil)
```

This statement sets the value of the variable `initial-scratch-message` to nil. Setting this value to nil (in your .emacs file) causes Emacs to start up without displaying basic usage information in the Scratch buffer, which is the default buffer you see if Emacs is started without specifying a file name on the command line.

Notice that rather than calling the variable `initial-scratch-message`, hyphens are used between the words. This is standard usage in Emacs-Lisp, ensuring that Emacs sees the variable as a unit. White space between words is always a signal telling Emacs that each word is a separate symbol.

# Functions

A *function* is a self-contained Lisp procedure. You could describe a function as a program that can be called by the Lisp interpreter to accomplish a specific task. Functions can contain other functions. You can think of a function as a module that can be plugged in to other functions. In a sense, functions are like abbreviations. It is theoretically possible to write a complex Lisp program without using any functions, but the labor of defining every routine would be immense.

Emacs makes use of several *primitive* functions, which are low-level procedures written in C. They are used just as Lisp functions are. From a user's point of view, the only difference is that primitive functions can't be changed. An example of a primitive function is +, the addition function discussed earlier.