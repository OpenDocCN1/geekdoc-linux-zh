As another example of the combination of . and *, the regular expression

e.*e

matches all the characters from the first e on a line to the last one.

Note that it doesn't necessarily match lines that start and end with an e, however because it's not left- or right-rooted (that is, it doesn't use ^ or $ in the pattern).

```
$ ed intro
248
1,$/[e.*e]++/
1,$p
Th+++n
Thompson and D+++S
in th+++ primary goals in
th+++ an
+++nt program
d+++nt.
```

Here's an interesting regular expression. What do you think it matches?

[A-Za-z] [A-Za-z]*

This matches any alphabetic character followed by zero or more alphabetic characters. This is pretty close to a regular expression that matches words and can be shown as below replace all words with the letter x while retaining all spaces and punctuation.

```
$ ed intro
248
1,$/[A-Za-z] [A-Za-z]*/X/g
1,$p
```

X X X X X X X X
X X X X X X X X
X X X 1960X. X X X X X
X X X X X X X X X
X X X X
X.

The only thing it didn't match in this example was the numeric sequence 1960. You can change the regular expression to also consider a sequence of digits as a word too, of course

```
$ ed intro
248
1,$/[A-Za-z0-9] [A-Za-z0-9]*/X/g
1,$p
X X X X X X X
X X X X X X X
X X X X.
X X X X X X X X
X X X X X X X
X X X X X
X.
```