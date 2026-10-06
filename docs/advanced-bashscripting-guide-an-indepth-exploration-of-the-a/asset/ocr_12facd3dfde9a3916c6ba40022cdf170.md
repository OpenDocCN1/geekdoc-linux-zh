# Advanced Bash–Scripting Guide

For a more elaborate example of passing arrays to functions, see Example A–8.

+   - Using the double parentheses construct, it is possible to use C-like syntax for setting and incrementing variables and in for while loops. See Example 10–12 and Example 10–17.
- A useful scripting technique is to repeatedly feed the output of a filter (by piping) to the same filter, with a different set of arguments and/or options. Especially suitable if this is tr.

```
# From "wstrings.sh" example.
wlist-"strings "$* | tr A-Z a-z | tr '[:space:]' Z | |
tr -cs '[[:alpha:]]' Z tr -s '\1\37\37' Z tr Z ' '
```

+   - The run-parts command is handy for running a set of command scripts in sequence, particularly in combination with cron or at.
- It would be nice to be able to invoke X–Windows widgets from a shell script. There have come to exist several packages that require it to do so, namely Xscript, Xmenu, and widtools. The first two of which seem longer to be de maint. Fortunately, it is still possible to extend widtools here.

![](bbox=[0.313, 0.403, 0.345, 0.423])

The widtools (widget) package requires the XForms to be installed. Additionally, the Makefile needs some judicious editing before the package will build on a typical Linux system. Finally, three of the six offered do not work (and, in fact, defunct)

For more effective scripting with widgets, try or wish (Tcl derivatives), PerlTk (Perl with Tk extensions), ksh (ksh with Tcl extensions), XForms4Perl (Perl with XForms extensions), or PyQt (Perl with Python with Qt extensions).

# 34.6. Odds

A script can recursively call itself. Indeed.

Example 34–9. A script that recursively calls itself

```
#!/bin/bash
# recurse.sh

# Can a script recursively call itself?
# Yes, but this is of little or no practical use
# except perhaps as a "proof of concept"

RANGE=10
MAXVAL=9
i=$RANDOM
let i=% $RANDOM  # Generate a random number between 0 and $MAXVAL.
```

# 34.6. Odds