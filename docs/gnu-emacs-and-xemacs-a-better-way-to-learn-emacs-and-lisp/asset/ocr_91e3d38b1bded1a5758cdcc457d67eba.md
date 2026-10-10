isp is short for *list processing*, these two words describe the action of a Lisp interpreter in a nutshell. A Lisp file has a surprisingly small number of basic building blocks, all of them lists made up of indivisible units called *atoms*. Another term for a Lisp list is *symbolic expression*, sometimes abbreviated as *s-expression* or just *expression*.

This chapter describes these basic elements. You will learn how to read a Lisp expression and then build your own. You will learn this material faster if you have an Emacs Scratch buffer handy; try out the expressions as you read. Emacs gives you immediate feedback if you evaluate an invalid expression in the Scratch buffer.

# Evaluation

To evaluate a Lisp expression is to feed it to the Lisp interpreter. This is much like running a compiled program. You can evaluate any of the following examples by typing them into the Scratch buffer, leaving the cursor to the right of the last parenthesis, and then pressing Ctrl-x Ctrl-e.

The Lisp interpreter's output appears in the minibuffer.

Evaluating a very simple Lisp expression returns nothing but the expression itself. The result of evaluation can be a value, a side effect such as copying a region or moving point, or an error message. Oddly enough, the side effect might be the actual result that the expression was written for. That might be the user's point of view, but to the Lisp interpreter, the returned value is the goal.

# Lists within Lists

When the interpreter begins the evaluation, it first looks for lists contained within the main list. These are evaluated first, and the returned value is substituted for the inner list when the outer list is processed. Here is a numerical example that illustrates this:

```
(\* 3 (- 20 4))
```

The contained list `(- 20 4)` is evaluated first, returning a value of `16`. The main expression now looks like this to the Lisp interpreter:

```
* 3 16
```

This is evaluated and returns a value of 48.