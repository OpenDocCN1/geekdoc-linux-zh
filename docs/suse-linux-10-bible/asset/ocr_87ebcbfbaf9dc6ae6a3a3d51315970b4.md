In the simplest case, you can use grep to output the lines of a file that contain a cer-particular string:

```
user@bible:-> cat file2
albatross
bat
hit
Batman
bathroom
debit
ding
doubt
dingbat
```

```
user@bible:-> grep bat file2
albatross
bat
bathroom
dingbat
```

The lines containing the exact string bat have been selected. Note that you don't see Batman in the output because by default grep is case-sensitive. To search-with case sensitivity, you use grep -i:

```
user@bible:-> grep -i bat file2
albatross
bat
Batman
bathroom
dingbat
```

# grep Options

In regular expression notation, a dot represents a single character, so an expression such as b.t represents a letter b followed by any other character, followed by a let-ter. The command that searches for any lines containing such a sequence:

```
user@bible:-> grep b.t file2
albatross
bat
hit
bathroom
debit
dingbat
```

To search for lines beginning with the letter d:

```
user@bible:-> grep "d file2
debit
ding
doubt
```