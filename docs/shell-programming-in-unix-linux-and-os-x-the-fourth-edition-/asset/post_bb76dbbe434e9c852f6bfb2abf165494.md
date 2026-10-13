
In the late 1960s one of the primary goals in the design of the Unix system was to create an environment that promoted efficient program development.

## Matching Zero or More Characters: The Asterisk (*)

The asterisk is used by the shell in filename substitution to match zero or more characters. In forming regular expressions, the asterisk is used to match zero or more occurrences of the *preceding* element of the regular expression (which may itself be another regular expression).

So, for example, the regular expression

```text
X*
```

matches zero, one, two, three, ... capital x’s while the expression

```text
XX*
```

matches one or more capital x’s, because the expression specifies a single x followed by zero or more x’s. You can accomplish the same effect with a + instead: it matches *one or more* of the preceding expression, so XX* and X+ are identical in function.

A similar type of pattern is frequently used to match one or more blank spaces in a line:

```text
$ ed lotspaces
85
1,$p
This       is    an   example   of   a
file    that    contains      a    lot
of     blank spaces
1,$s/ */ /g
1,$p
This       is    an   example   of   a
file    that    contains      a    lot
of     blank spaces
```

Change multiple blanks to single blanks

The ed command

```text
1,$s/ */ /g
```

told the program to substitute all occurrences of a space followed by zero or more spaces with a single space—in other words, to collapse all whitespace into single spaces. If it matches a single space, there’s no change. But if it matches three spaces, say, they’ll all be replaced by a single space.

The regular expression

```text
.*
```

is often used to specify zero or more occurrences of *any* characters. Bear in mind that a regular expression matches the *longest* string of characters that match the pattern. Therefore, used by itself, this regular expression always matches the *entire* line of text.

As another example of the combination of `.` and `*`, the regular expression

```text
e.*e
```

matches all the characters from the first `e` on a line to the last one.

> Note that it doesn’t necessarily match only lines that start and end with an `e`, however, because it’s not left- or right-rooted (that is, it doesn’t use `^` or `$` in the pattern).

```text
$ ed intro
248
1,$s/e.*e/+++/
1,$p
Th+++n
Thompson and D+++s
 in th+++ primary goals in
 th+++ an
 +++nt program
 d+++nt.
```

Here’s an interesting regular expression. What do you think it matches?

```text
[A-Za-z][A-Za-z]*
```

This matches any alphabetic character followed by zero or more alphabetic characters. This is pretty close to a regular expression that matches words and can be used as shown below to replace all words with the letter X while retaining all spaces and punctuation.

```text
$ ed intro
248
1,$s/[A-Za-z][A-Za-z]*/X/g
1,$p
X X X X X X X X
X X X X X X X
X X X 1960X. X X X X X
X X X X X X X X X
X X X X X
X.
```

The only thing it didn’t match in this example was the numeric sequence 1960. You can change the regular expression to also consider a sequence of digits as a word too, of course:

```text
$ ed intro
248
1,$s/[A-Za-z0-9][A-Za-z0-9]*/X/g
1,$p
X X X X X X X X
X X X X X X X
X X X X X X X X X X
X X X X X X X X X X X
X X X X X
X.
```

We could expand on this to consider hyphenated and contracted words (for example, don’t), but we’ll leave that as an exercise for you. As a point to note, if you want to match a dash character inside a bracketed choice of characters, you must put the dash immediately after the left bracket (but after the inversion character `^` if present) or immediately before the right bracket for it to be properly understood. That is, either of these expressions

```text
[-0-9]
```

```text
[0-9-]
```

matches a single dash or digit character.

In a similar fashion, if you want to match a right bracket character, it must appear after the opening left bracket (and after the `^` if present). So

```text
[]a-z]
```

matches a right bracket or a lowercase letter.

## Matching a Precise Number of Subpatterns: `\{...\}`

In the preceding examples, you saw how to use the asterisk to specify that zero or more occurrences of the preceding regular expression are to be matched. For instance, the regular expression

```text
xx*
```

means match an x followed by zero or more subsequent occurrences of the letter x. Similarly,

```text
xxx*
```

means match at least two consecutive x’s.

Once you get to this point, however, it ends up rather clunky, so there is a more general way to specify a precise number of characters to be matched: by using the construct

```text
\{min,max\}
```

where min specifies the minimum number of occurrences of the preceding regular expression to be matched, and max specifies the maximum. Notice that you need to escape the curly brackets by preceding each with a backslash.

The regular expression

```text
x\{1,10\}
```

matches from one to 10 consecutive x’s. Whenever there’s a choice, the largest pattern is matched, so if the input text contains eight consecutive x’s, that is how many will be matched by the preceding regular expression.

As another example, the regular expression

```text
[A-Za-z]\{4,7\}
```

matches a sequence of alphabetic letters from four to seven characters long.

Let’s try a substitution using this notation:

```text
$ ed intro
248
1,$s/[A-Za-z]\{4,7\}/X/g
1,$p
The X Xng X was Xed by Ken
Xn and X X at X XX
in the X 1960s. One of the X X in
the X of the X X was to X an
XX X Xd Xnt X
XX.
```

This invocation is a specific instance of a global search and replace in ed (and, therefore, also in vi): *s/old/new/*. In this case, we add a range of 1,$ beforehand and the g flag is appended to ensure that multiple substitutions will occur on each line, as appropriate.

A few special cases of this special construct are worth noting. If only one number is enclosed by braces, as in

```text
\{10\}
```

that number specifies that the preceding regular expression must be matched *exactly* that many times. So

```text
[a-zA-Z]\{7\}
```

matches exactly seven alphabetic characters; and

```text
.\{10\}
```

matches exactly 10 characters no matter what they are:

```text
$ ed intro
248
1,$s/^.*\{10\}//
1,$p
perating system was pioneered by Ken
nd Dennis Ritchie at Bell Laboratories
e 1960s. One of the primary goals in
 of the Unix system was to create an
t that promoted efficient program
t.
```

*Delete the first 10 chars from each line*

```text
$ ed intro
248
1,$s/.\{5\}$//
1,$p
perating system was pioneered b
nd Dennis Ritchie at Bell Laborat
 e 1960s. One of the primary goa
 of the Unix system was to crea
t that promoted efficient pr
t.
```

*Delete the last 5 chars from each line*

Note that the last line of the file didn’t have five characters when the last substitute command was executed; therefore, the match failed on that line and thus was left alone because we specified that *exactly* five characters were to be deleted.

If a single number is enclosed in the braces, followed immediately by a comma, then *at least* that many occurrences of the previous regular expression must be matched, but no upper limit is set. So

```text
+\{5,\}
```

matches at least five consecutive plus signs. If more than five occur sequentially in the input data, the largest number is matched.

```text
$ ed intro
248
1,$s/[a-zA-Z]\{6,\}/X/g
1,$p
The Unix X X was X by Ken
X and X at Bell X
in the late 1960s. One of the X goals in
the X of the Unix X was to X an
X that X X X
X.
```

*Change words at least 6 letters long to X*

## Saving Matched Characters: `\(...\)`

It is possible to reference the characters matched against a regular expression by enclosing those characters inside backslashed parentheses. These captured characters are stored in pre-defined variables in the regular expression parser called *registers*, which are numbered 1 through 9.

This gets a bit confusing, so take this section slowly!

As a first example, the regular expression

```text
^\(.\)
```

matches the first character on the line, whatever it is, and stores it into register 1.

To retrieve the characters stored in a particular register, the construct `\n` is used, where *n* is a digit from 1 to 9. So the regular expression

```text
^\(.\)\1
```

initially matches the first character on the line and stores it in register 1, then matches whatever is stored in register 1, as specified by the `\1`. The net effect of this regular expression is to match the first two characters on a line if *they are both the same character*. Tricky, eh?

The regular expression

```text
^\(.\).*\1$
```

matches all lines in which the first character on the line (`^.`) is the same as the last character on the line (`\1$`). The `.*` matches all the characters in-between.
