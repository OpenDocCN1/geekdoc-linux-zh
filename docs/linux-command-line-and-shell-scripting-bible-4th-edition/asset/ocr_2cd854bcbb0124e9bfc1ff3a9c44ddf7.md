added to the grep command. If you look over the man pages for the grep command, you'll see how versatile it is.

If you want to reverse the search (output lines that don't match the pattern), use the -v parameter:

```
```
$ grep -v t file1
one
four
five
$
```
```

If you need to find the line numbers where the matching patterns are found, use the -n parameter:

```
```
$ grep -n t file1
2:two
3:three
$
```
```

If you just need to see a count of how many lines contain the matching pattern, use the -c parameter:

```
```
$ grep -c t file1
2
$
```
```

If you need to specify more than one matching pattern, use the -e parameter to specify each individual pattern:

```
```
$ grep -e t -e f file1
two
three
four
five
$
```
```

This example outputs lines that contain either the string t or the string f.

By default, the grep command uses basic Unix-style regular expressions to match patterns. A Unix-style regular expression uses special characters to define how to look for matching patterns. For a more detailed explanation of regular expressions, see Chapter 20, “Regular Expressions.”