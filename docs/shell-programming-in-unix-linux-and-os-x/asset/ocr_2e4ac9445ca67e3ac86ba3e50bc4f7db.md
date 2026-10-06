# Regular Expressions

Note that the last line of the file didn't have five characters when the last substitute command was executed; therefore, the match failed on that line and thus was left alone because we specified *exactly* five characters were to be deleted.

If a single number is enclosed in the braces, followed immediately by a comma, then at least that many occurs of the previous regular expression must be matched, but no upper limit is set. So

+{5,}
matches at least five consecutive signs. If more than five occur sequentially in the input data, the largest number is matched

```
$ ed ito
248
1,$\[a-zA-Z]\{6,\}/X/g
1,$
```

Change words at least 6 letters long to X
The Unix X was X by Ken
X and X X at Bell X
in the late 1960s. One of the X goals in
the X of the Unix X was to An X
X X X

# Saving Matched Characters: \(\..\)

It is possible to reference the characters matched against a regular expression by enclosing them inside backslashed parentheses. These captured characters are stored in pre-defined variables in the regular expression parser called *registers*, which are numbered 1 through 9.

This gets a bit confusing, so take this slowly!
As a first example, the regular expression

\(\.)
matches the first character on the line, whatever it is, and stores it into register 1.

To retrieve the characters stored in a particular register, the construct \*n* is used, where *n* is a digit from 1 to 9. So the regular expression

\(\.).\1
initially matches the first character on the line and stores it in register 1, then matches-ever is stored in register 1, as specified by the \1. The net effect of this regular expression is to match the first characters on a line if *they are both the same character*. Tricky, eh?

The regular expression
\(\.).*\1$
matches all lines in which the first character on the line (.) is the same as the last character on the line (\1$). The . * matches all characters in-between.