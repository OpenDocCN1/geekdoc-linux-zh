![](bbox=[0.07, 0.16, 0.17, 0.27])

The use of single quotes tells the shell to leave these characters alone and to pass them to the program. Single quotes are necessary whenever using any of the special characters.

The dollar sign indicates that you want to match a pattern at the end of the line. In the following command, for example, any lines ending with the word “hello” result in a match using the preceding regular expression:

```
grep 'hello$' data.txt
```

To look for a pattern that begins a word, use \<. For example, the following command searches for words that begin with “ki” in the file data.txt:

```
grep '\<ki' data.txt
```

To find the pattern “wee,” but only at the end of a word, use:

```
grep 'wee\>' data.txt
```

In Table 9-3, notice that the period matches any single character except the newline character (i.e., ASCII character value x10). This comes in handy if, for example, you’re searching for all the lines that contain the letter “C” followed by two letters and end in “s”; in this case, the regular expression is:

```
grep 'C..s' data.txt
```

This expression matches patterns such as “Cats,” “Cars,” and “Cris” in the file data.txt.

If you want to specify a range of characters, use a hyphen to separate the beginning and end of the range. When you specify the range, the order must be the same as in the ASCII code. For example, to search for all lines that contain a “B” followed by any single lowercase letter, use the following command:

```
grep 'B[a-z]' data.txt
```

You can also specify more than one range of characters in the same pattern. For example, the following command selects all lines that contain the letter “B” that are followed by an uppercase or lowercase letter.

```
grep 'B[A-Za-z]' data.txt
```