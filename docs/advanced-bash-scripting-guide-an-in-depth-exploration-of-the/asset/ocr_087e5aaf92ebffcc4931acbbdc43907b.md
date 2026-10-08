# # Advanced Bash-Scripting Guide

```
# -----------------
# Chet Ramey seems to have bunch of undocumented C-style
# constructs into Bash (actually adapted from ksh, pretty much).
# In the Bash doc, Ramey calls (( )) shell arithmetic,
# but it goes far beyond that.
# Sorry, Chet, the secret is out.

# See also "for" and "while" loops using the (( )) construct.
# These work only with version 2.04 or later of Bash.

exit
```

See also [Example 11-13] and [Example 8-4]

# ## 8.4. Operator Precedence

In a script, operations execute in order of *precedence*: the higher precedence operations execute before the lower precedence ones. [40]

Table 8-1. Operator Precedence

| Operator | Meaning | Comments |
| --- | --- | --- |
| var++ var-- | post-increment, post-decrement | HIGHEST PRECEDENCE C-style operators |
| ++var --var | pre-increment, pre-decrement | |
| ! ~ | negation | logical / bitwise, inverts sense of following operator |
| ** | exponentiation | arithmetic operation |
| * / % | multiplication, division, modulo | arithmetic operation |
| + - | addition, subtraction | arithmetic operation |
| << >> | left, right shift | bitwise |
| -z -n | unary comparison | string is/is-not null |
| -e -f -t -x, etc. | unary comparison | file-test |
| -lt > -gt <= -le >= -ge | compound comparison | string and integer |
| -nt -ot -ef | compound comparison | file-test |
| == -eq != !=ne | equality / inequality | test operators, and integer |
| & | AND | bitwise |
| ^ | XOR | exclusive OR, bitwise |
| ! | OR | bitwise |

Chapter 8. Operations and Related Topics 81