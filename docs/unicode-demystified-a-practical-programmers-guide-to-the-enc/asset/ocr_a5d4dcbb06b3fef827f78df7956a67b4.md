# (End-of-Word Indicator)

This pair of characters matches the end of a word. The typical command /s\ finds the next word that ends with a backslash (\) an s. Whereas (\) is used to turn off the special meaning of a character, the sequence \> has a special meaning, and > alone does not.

# (Beginning-of-Word Indicator)

This pair of characters matches the beginning of a word. The command /<The finds the next word that begins with The. The beginning-of-word indicator uses the backslash in an, atypical way as the end-of-word indicator.

# (Save Pattern)

These delimiters save whatever is between them into a special holding buffer. This buffer can then be referred to call up to nine previously saved patterns by using a backslash followed by a number (\1 through9).

# (Zero or More Occurrences)

This character is a modifier that will match zero or more occurrences of the character immediately preceding it. The command /dis*m will match the string followed by zero or more s followed by an m. Examples of successful matches would include dim dis or diss

# (Character-Class Definition)

Brackets surrounding two or more characters match any single character located between the brackets. The command /dis[ck] finds the next occurrence of either disk or disc.

There are two special characters you can use within a character-class definition. A caret^) as the first character following the left bracket defines the character class to be any but the following characters. The hyphen between two characters indicates a range of characters. Refer to the examples in Table 10-4.

# Substituting One String for Another

A Substitute command, searches for a string just as the / command does, allowing the same special characters that the previous section discussed changes it. When it finds a string, the syntax of the Substitute command is

```
:g|address|s/search-string/replacement-string[/option]
```

As with all commands that begin with a colon, vim executes a Substitute command from the status line.