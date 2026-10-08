fgets is a means of reading a line of input, stdin is the standard input file (usually your terminal), and buffer is an array of characters.

One weakness of the if statement is that, with else, the parsing can be tricky. Consider this case:

```
if (a-b) if (c<d) { /* Do something */ }
else { /* Do something else */ }
```

This is a perfectly valid statement in C but very ambiguous. The else clause to be executed is bound with the symbols if a-b and c<d? Or is it executed only if a->b? This depends on the compiler, but it usually defaults to the highest valued unmatched condition, that is, a->b. If you mean the former, though, you can force that result by putting the second if, with the else, in a statement:

```
if (a-b)
  if (c<d)
    {
      /* Do something */
    }
  else
    {
      /* Do something else */
    }
```

You similarly can force the other interpretation with:

```
if (a-b)
  if (c<d)
    {
      /* Do something */
    }
else
  {
    /* Do something else */
  }
```

An alternative forcing is to have an empty block with {} symbols and nothing in between:

```
if (a-b)
  if (c<d)
    {
      /* Do something */
    }
  else
    {
      /* Do something else */
    }
```

![](bbox=[0.065, 0.893, 0.145, 0.965])