This example looks for the regular expression cat or dog in the data stream. You can't place any spaces within the regular expressions and the pipe symbol, or they'll be added to the regular expression pattern.

The regular expressions on either side of the pipe symbol can use any regular expression pattern, including expression classes, to define the text:

```
$ echo "He has a hat." | awk '/[ch]at|dog/(print $0)'
He has a hat.
$
```

This example would match cat, hat, or dog in the data stream text.

# Grouping expressions

Regular expression patterns can also be grouped using parentheses. When you group a regular expression pattern, the group is treated as a standard character. You can apply a special character to the group just as you would to a regular character. For example:

```
$ echo "Sat" | awk '/[Sat(urday)?/(print $0)'
Sat
$ echo "Saturday" | awk '/Sat(urday)?/(print $0)'
Saturday
```

The grouping of the day ending with the question mark allows the pattern to match the full day name or the abbreviated name.

It's common to use grouping along with the pipe symbol to create groups of possible matches:

```
$ echo "cat" | awk '/(c|b)a(b|t)/(print $0)'
cat
$ echo "cab" | awk '/(c|b)a(b|t)/(print $0)'
cab
$ echo "bat" | awk '/(c|b)a(b|t)/(print $0)'
bat
$ echo "bab" | awk '/(c|b)a(b|t)/(print $0)'
bab
$ echo "tab" | awk '/(c|b)a(b|t)/(print $0)'
$
$ echo "tac" | awk '/(c|b)a(b|t)/(print $0)'
$
```

The pattern (c|b)a(b|t) matches any combination of the letters in the first group along with any combination of the letters in the second group.