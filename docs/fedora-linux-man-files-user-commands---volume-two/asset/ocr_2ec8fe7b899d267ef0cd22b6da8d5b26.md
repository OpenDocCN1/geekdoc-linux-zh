# USAGE

Only the differences between GNU **eqn** and Unix eqn are described here.

GNU **eqn** emits Presentation MathML output when invoked with the -T\~MathML option.

GNU eqn sets the input token ... as three periods or low dots, rather than the three centered dots of classic eqn. To get three centered dots, write \textbf{cdots} or \textbf{cdot cdot cdot}.

Most of the new features of the GNU **eqn** input language are based on TeX. There are some references to the differences between TeX and GNU **eqn** below; these may safely be ignored if you do not know TeX.

# Controlling delimiters

If not in compatibility mode, **eqn** recognizes

```
    \textbf{delim on}
```

to restore the delimiters which have been previously disabled with a call to ‘\textbf{delim off}’. If delimiters haven’t been specified, the call has no effect.

# Automatic spacing

**eqn** gives each component of an equation a type, and adjusts the spacing between components using that type. Possible types are:

+   ordinary
+       an ordinary character such as ‘1’ or ‘x’;

+   operator
+       a large operator such as ‘$\hat{L}$’;

+   binary
+       a binary operator such as ‘+’;

+   relation
+       a relation such as ‘=’;

+   opening
+       a opening bracket such as ‘(’;

+   closing
+       a closing bracket such as ‘)’;

+   punctuation
+       a punctuation character such as ‘,cl;

+   inner
+       a subformula contained within brackets;

+   suppress spacing
+       that suppresses automatic spacing adjustment.