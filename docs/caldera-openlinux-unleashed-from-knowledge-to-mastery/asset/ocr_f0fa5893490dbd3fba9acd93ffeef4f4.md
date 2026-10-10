In the first *expr*, the Tcl parser does the substitution. In the second *expr*, the expression evaluator does the substitution. In the second case, the substituted variable must hold only a simple value. (That is, monkey business like set a `*5*6*7` won't work. In any case, you should avoid tricks like this.)

# ## Built-in Functions

Tcl has many built-in functions such as `sin`, `exp`, and so on. For details, see `expr(n)` (after fixing your `MANPATH`).

# ## Lists

Tcl uses lists to represent collections. A *list* is a sequence of elements.

In its simplest form, a list is a space-separated collection of words. For example, the string Hop Skip Jump is a list with three elements.

# ## Extracting List Elements

The `lindex` command extracts a particular element from a list. It takes as arguments a list and an index and returns the appropriate element. An index is an integer with 0 corresponding to the first element, 1 to the second, and so on, as shown in the following:

```
```
% lindex {Hop Skip Jump} 1
Skip
```
```

When you type a list to the Tcl interpreter, you often enclose the elements in braces to ensure that the list is interpreted as a single word. These braces are not part of the list itself, as the following shows:

```
```
% set x {Hop Skip Jump}
Hop Skip Jump
% lindex $x 2
Jump
```
```

# ## Creating Lists

The `concat` command concatenates a number of lists. Consider the following example:

```
```
% concat {1 2 3} 4 5 {6 7}
1 2 3 4 5 6 7
```
```

`concat` is given four lists (note that the bare words `4` and `5` are treated as single-element lists) and returns a list consisting of all the elements in the original list.

The `list` command, on the other hand, joins all of its arguments together so that each argument becomes a single element of the resulting list. The following are some examples: