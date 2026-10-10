refers. In a sense, an alist is a simple database. There can be any number of cons cells in an associated list. The following example has only two:

```
```
(setq tools-alist
      '((wrench . nut) (hammer . nail)))
```
```

This Lisp expression creates a new variable named tools-alist. This variable refers to the association list on the second line. The periods and extra spaces separating the respective keys (wrench and hammer) and their associated values (nut and nail) indicate that the association list is written in dotted-pair notation, an alternative method of representing a list that is often used in association lists. The period explicitly separates a cons cell's car and cdr. The preceding list written in standard notation looks like this:

```
```'
('wrench nut) (hammer nail))
```
```

assoc is the most commonly used of a group of functions that look for matches in an alist. Here is this function being used to find a match in the preceding alist:

```
```
(assoc 'hammer tools-alist)
```
```

Evaluation returns this value:

```
```
(hammer . nail)
```
```

An English translation of this assoc expression might read something like this:

> > In the associated list named tools-alist, which value does the key hammer match?

# # The progn Function

progn is a wrapper function in the same way that the save-excursion function in dos-unix is (see Chapter 6). Each function or other expression following progn is evaluated one by one, but the values returned are discarded, with the exception of the very last one. Typically, the changes made by the earlier-than-last functions are (from the interpreter's point of view) just side effects, but they are needed by the overall program or function that contains the progn function block. The side-effects might be such things as minibuffer messages, moved point position, or deletions of some portion of the buffer.

The end result is that the value returned from the last Lisp statement in the progn-wrapped block of code is passed to the next phase following it.

The syntax is as follows:

```
```
(progn (expression1) (expression2) (expression3))
```
```