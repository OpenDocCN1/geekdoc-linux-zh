# …or to the End of a List

An analogous function is used to insert a list at the end of a list. This one is called `append`, and its usage is similar to that of `cons`. Here is an example:

```
(append '(oak ash) '(birch pine))
```

The output is

```
(oak ash birch pine)
```

As you can see, the second list is attached to the end of the first.

An example will show how `cons` can be used to add to one of Emacs’ variables. The value of the variable `load-path` is an associated list of directories in which Emacs will look for Lisp files to load. This `setq` statement uses `cons` to add a new directory to the front of the list:

```
(setq load-path (cons [new directory] load-path))
```

Evaluation of this statement forces Emacs to look in the new directory for a Lisp file before checking the original directories in the list.

# Saving an Excursion

When you write a text-manipulation function, the position of point often moves away from the starting point, leaving point at a new place in the buffer. You might prefer that, after you run a function, the point position return to the starting point—which, after all, is where you were editing.

The `save-excursion` built-in function is the answer to this common problem. This function acts as a wrapper around the main body of a function, allowing the point and mark positions to go wherever they need to go, but returning them to their original positions when the function operation is complete.

To illustrate this, here is a modification of the `dos-unix` function from earlier in the chapter:

```
(defun dos-unix ()
*Strip DOS carriage return characters from a buffer."
(interactive)
(save-excursion
(goto-char (point-min))
(while (search-forward "\r" nil t) (replace-match ""))
message "Operation complete"))
```