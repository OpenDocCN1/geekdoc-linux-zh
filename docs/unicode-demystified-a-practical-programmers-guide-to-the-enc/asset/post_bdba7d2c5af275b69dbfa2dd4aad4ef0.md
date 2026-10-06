
# Substitute Command Examples

| | |
|---|---|
| s | Substitutes one or more characters for the current character |
| s$ | Substitutes one or more characters for current line |
| 5s | Substitutes one or more characters for five characters, starting with the current character |

# Searching and Substituting

Searching for replacing a character, a string of text, or a string that is matched by a regular expression is a key feature of any editor. The vim editor provides simple commands for searching for a character on the current line. It also provides complex commands for searching for and optionally substituting for single and multiple occurrences of strings or regular expressions anywhere in the Work buffer.

# Searching for a Character

You can search and move the cursor to the next occurrence of a specified character on the current line using the Find command. Refer to “Moving the Cursor to a Specific Character” on page 429.

The next two commands are used in the same manner as the Find command. The t command places the cursor on the character before the next occurrence of the specified character, whereas the T command places it on the character after the previous occurrence of the specified character.

A semicolon (;) repeats the last f, t, or T command.

You can combine these search commands with other commands. For example, the command d2fq deletes the text from the location of the cursor to the second occurrence of the letter q on the current line.

# Searching for a String

Forward and backward search commands just discussed are restricted to searches within the current line. The vim editor can also search backward or forward through the Work buffer to find a specific string of text or a string that matches a regular expression (see Appendix A). To find the next occurrence of a string (forward), press the forward slash (/) key, enter the text you want to find (called the search string), and press RETURN. When you press the slash key, vim displays a slash on the status line. As you enter the string of text, it too is displayed on the status line. When RETURN, vim searches for the string. If it finds, vim positions the cursor on the first character of the string. If you use a question mark (?) in the forward slash, vim searches for the previous occurrence of the string. If you need to include a slash in a forward search or a question mark in a backward search, you must quote it by preceding it with a backslash (\).

The N and n keys keep the last search without the need for you to enter the search again. The n key repeats the original string exactly, and the N key repeats the search in the opposite direction of the original search.

Normally, if you are searching forward and vim does not find the search string before it gets to the end of the Work buffer, vim wraps around and continues the search at the beginning of the Work buffer. During a backward search, vim wraps around the Work buffer to the end. Also, vim performs case-sensitive searches. Refer to “Wrap Scan’ (page 454) and “Ignore case in searches” (page 454) for information about how to change these search parameters.

# Special Characters in Search Strings

Because the search string is a regular expression, some characters take on a special meaning within the search string. The following paragraphs list some of these characters. The first two (^ and $) always have their meanings within a search string unless you quote them (page 433), and the rest can have their special meanings within a search turned off by a single command. Refer to “Allow special characters in searches” on page 454.

- ^ (Beginning-of-Line Indicator)
When the first character in a search string is a caret, or circumflex, it matches the beginning of a line. The command /^ finds the next line that begins with the string.

- $ (End-of-Line Indicator)
Similarly, a dollar sign matches the end of a line. The command /$$ finds the next line that ends with an exclamation point.

- . (Any-Character Indicator)
A period matches any character, anywhere in the search string. The command /.. finds line, followed, like, included, all memory, or any other word or character string that contains an I followed by two characters and an e. To search for a period, use a backslash to quote the period (\.).

- \> (End-of-Word Indicator)
This pair of characters matches the end of a word. The command /\s\ finds the next word that ends with a backslash (\) an s. Whereas (\ is used to turn off the special meaning of a character, the sequence \> has a special meaning, and > alone does not.

- \< (Beginning-of-Word Indicator)
This pair of characters matches the beginning of a word. The command /< finds the next word that begins with The. The beginning-of-word indicator uses the backslash in an, atypical way as the end-of-word indicator.

- () (Save Pattern)
These delimiters save whatever is between them into a special holding buffer. This buffer can then be referred to call up to nine previously saved patterns by using a backslash followed by a number (\1 through \9).

- * (Zero or More Occurrences)
This character is a modifier that will match zero or more occurrences of the character immediately preceding it. The command /dis*m will match the string followed by zero or more s followed by an m. Examples of successful matches would include dim dis or diss

- [] (Character-Class Definition)
Brackets surrounding two or more characters match any single character located between the brackets. The command /dis[ck] finds the next occurrence of either disk or disc.

There are two special characters you can use within a character-class definition. A caret^) as the first character following the left bracket defines the character class to be any but the following characters. The hyphen between two characters indicates a range of characters. Refer to the examples in Table 10-4.

# Substituting One String for Another

A Substitute command, searches for a string just as the / command does, allowing the same special characters that the previous section discussed changes it. When it finds a string, the syntax of the Substitute command is

```
:g|address|s/search-string/replacement-string[/option]
```

As with all commands that begin with a colon, vim executes a Substitute command from the status line.

# Search Examples 10-4

| | | Examples |
|---|---|---|
| /and | Finds the next occurrence of the string | Examples: sand and standard slander and |
| ^<and\> | Finds the next occurrence of the word and | Example: and |
| ^/The | Finds the next line that starts with The | Examples: The... There... |
| ^\[0-9][0-9]\] | Finds the next line that starts with a two-digit number followed by a right parenthesis | Examples: 77... 01... 15... |
| ^<adr> | Finds the next word that starts with an a, d, or r | Examples: apple drive road argument right |
| ^\[A-Za-z\] | Finds the next line that starts with an upper-lowercase letter | Examples: will not find a line starting with the number 7... Dear Mr. Jones ... in the middle of a sentence like this ... |

# Substitute Address
If you do not specify an address, Substitute searches only the current line. If you use a single line as the address, Substitute searches that line. If the address is two lines separated by comma, Substitute searches those lines and the lines between. Refer to “Line numbers” on page 453 if you want to display line numbers. Any place a line number is allowed in the address, you may also use an address-string enclosed between slashes. / The vim editor operates on the next line that the address-string matches. When you precede the first slash of the address-string with the letter g (for global), vim operates on all lines in the file that the address-string matches. (This g is not the same as the one that goes at the end of the Substitute command to cause multiple replacements on a single line like “Searching for and Replacing Strings”).
Within the address, a period represents the current line, a dollar sign represents the last line in the Work buffer, and a percent sign represents the entire Work buffer.
