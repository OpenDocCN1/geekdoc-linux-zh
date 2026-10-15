# Can you give me some examples of how to use sed?

By combining both addresses and commands, you form a complete sed command, which might look something like this:

```
sed -e '/foo/d' myfile
```

This sed invocation would delete every line that contains the word "foo" and print the results to standard out. This is an example of using zero addresses, which results in attempting the match on every single line. Another example would be:

```
sed -e '50d' myfile
```

which would result in deleting line 50 of myfile, while

```
sed -e '50,$d' myfile
```

would delete everything from line 50 to the end ($ refers to the last line in the stream). Another common task involves replacing one pattern of text with another. This is done using the s command, instead of the d above, and might look similar to the following:

```
sed -e 's/foo/bar/' myfile
```

This example would substitute the first occurrence of the word "foo" with the word "bar" on each line. If you wanted to replace multiple occurrences on the same line, you would need to append a g after the command, as in the following:

```
sed -e 's/foo/bar/g' myfile
```

Regular expression patterns can be used in the search space above (instead of "foo", for example), which can add more power to your editing. If you wanted to place a series of asterisks in front of specific lines, for example, you might use:

```
sed -e '/foo/s/^/*** /' myfile
```

This would find every line with the word "foo" in it, and replace the beginning of the line (^ is a special symbol that refers to the beginning of the line) with three asterisks.

A final word of warning is in order. Since sed is stream-oriented, it does not read the entire input file into