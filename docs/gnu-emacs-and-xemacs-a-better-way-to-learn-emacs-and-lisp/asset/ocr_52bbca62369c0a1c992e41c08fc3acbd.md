This, in English, is “three times ten,” and it yields a final value of 30.

If the expression looks like this instead:

```
'(* 3 (+ 5 5))
```

the evaluation would return this:

```
(* 3 (+ 5 5))
```

rather than 30 because the single quote forces the interpreter to accept the * and + as meaningless characters rather than arithmetic symbols.

Every list and list-within-a-list is enclosed in parentheses. This is a Lisp convention that helps the interpreter find the boundaries of any list. A list can be pages long and can contain many other lists. The Emacs-Lisp interpreter burrows down to the innermost list and evaluates its way out. Once the inner lists have been evaluated, the interpreter works its way from left to right through the list, substituting the values stored in memory earlier for each contained list.

# Numbers and Strings

Emacs-Lisp recognizes both integers and floating-point numbers, distinguishing between the two by the presence or absence of a decimal point. For example, 3 and 236 are treated as integers, while 37.66 and 21.0 are seen as floating-point numbers.

Strings are most often used when a message needs to be displayed to the user. The Emacs minibuffer messages are good examples. When you see the prompt I-search: in the minibuffer, you are seeing a string variable from a Lisp file named isearch.el, one of the core Emacs-Lisp files.

Strings are also used when a Lisp program needs a changeable chunk of text. An example might be a Lisp-based add-on for Emacs that adds e-mail capabilities to the editor. Such a Lisp program would need to be able to use the user’s e-mail address. The Lisp program doesn’t need to know the address; this data is saved to be pasted into the From: header of a e-mail message. When text is enclosed in double quotes (making the text a string to the Lisp interpreter), the text is handled as a unit. Remember that a string is also an atom, an indivisible block.

# Symbols

A symbol is a unique name in a Lisp expression. It is nothing more than a word or character that most often refers to a Lisp function or variable, though symbols can refer to anything. One symbol can refer to both a function or variable in the same