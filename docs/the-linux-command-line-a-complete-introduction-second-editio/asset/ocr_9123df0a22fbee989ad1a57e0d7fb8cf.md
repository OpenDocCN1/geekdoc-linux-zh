indicate negation; the second is the dash (-), which is used to indicate a character range.

# Negation

If the first character in a bracket expression is a caret (^), the remaining characters are taken to be a set of characters that must not be present at the given character position. We do this by modifying our previous example, as follows:

```
[me@linuxbox ~]$ grep -h '[ ^bg]zip' dirlist*.txt
bunzip2
gunzip
funzip
gpg-zip
preunzip
prezip
prezip-bin
unzip
unzipsfx
```

With negation activated, we get a list of files that contain the string zip preceded by any character except b or g. Notice that the file zip was not found. A negated character set still requires a character at the given position, but the character must not be a member of the negated set.

The caret character invokes negation only if it is the first character within a bracket expression; otherwise, it loses its special meaning and becomes an ordinary character in the set.

# Traditional Character Ranges

If we wanted to construct a regular expression that would find every file in our lists beginning with an uppercase letter, we could do this:

```
[me@linuxbox ~]$ grep -h '^[A BCDEFGHIJKLMNOPQRSTUVWXYZ]' dirlist*.txt
```

It’s just a matter of putting all 26 uppercase letters in a bracket expression. But the idea of all that typing is deeply troubling, so here is another way.