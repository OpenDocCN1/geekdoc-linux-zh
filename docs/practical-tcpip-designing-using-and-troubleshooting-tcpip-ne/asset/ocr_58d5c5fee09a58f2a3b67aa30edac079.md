+   • a “*” after a portion of the pattern means “zero or more occurrences of the element of the pattern that precedes the *.” We haven't defined what “element” means – you'll have to look at Web Appendix 16 for that, but here are a couple of examples: “B[a-z]*” matches any word starting with uppercase B, and “[0-9]*” matches a string of zero or more digits

+   • a “+” after a portion of the pattern means “one or more occurrences of the element of the pattern that precedes it,” e.g. “[0-9]+” matches a string of digits, but doesn't match the empty string

+   • a “?” after a portion of the pattern means “zero or one occurrences of the element of the pattern that precedes it,” e.g. “[0-9]?” matches a single digit or the empty string.

+   • a “|” between two patterns means “match either of these”. E.g. “cat|dog” matches “cat” or “dog”.

Don't be put off by the complexity of the patterns. Most of the time you just need the ordinary characters, which include alphanumerics, numerics, and spaces; these match exactly as you type them. Later on, if you need to search for wildcards, etc., you can experiment with more sophisticated patterns. Here are some examples

Look for any traffic on port 80 that contains the string “HTTP/1.1”, irrespective of whether it's upper- or lowercase:

```
ngrep -i "http/1.1" port 80
```

Show any packets that contain the POP commands LIST, RETR, or DELE, ignoring case:

```
ngrep -i 'retr|list|dele'
```

> Tip: if you're new to regular expressions and have a Linux system, you can experiment using egrep. Linux's extended grep program, it uses the same regexs as ngrep. egrep reads lines from input files or its standard input (your keyboard in the example below). If the input line matches the pattern you specified, it's copied to the standard output (printed on your terminal). If the line doesn't match it's not printed. Below is an example. For clarity we've indented egrep's output.

```
alice% egrep -i '^retr|list|dele'
retrie
retrieve
firetrap
deleted
yodeler
yodeler
listing
listing
vocalist
```

The example shows an easy mistake to make: the “^” applies only to the retr part of the pattern, so retr is matched only at the beginning of a line, but list and dele are matched anywhere in the line. If you intended to match any of the words only at the beginning of the line, the correct command is “egrep -i '^(retr|list|dele)'” (See Notes for details).