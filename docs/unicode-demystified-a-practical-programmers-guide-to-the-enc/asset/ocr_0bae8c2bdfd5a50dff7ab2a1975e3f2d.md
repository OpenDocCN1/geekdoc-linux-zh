The first command following do displays the string represented by number. The next command uses the expr utility to increment the value of number by one. The expr converts its arguments to numbers, adds them, converts to characters, and sends them to standard output. The $(...) causes the enclosed command to be replaced by the output of the command (command substitution). This value is assigned to the variable number. The first time through the loop, number has a value of zero, so expr converts the strings 0 and 1 to numbers, adds them, and converts back to a string (1). The shell assigns this value to the variable number. The done statement closes the loop and returns control to the while statement to start the loop again. The final echo causes count to send a NEWLINE character to the display (rather than immediately following the leftmost column on on 9).

# Optional

# The spell_check Script

The aspell utility checks the words in a file against a dictionary of correctly spelled words. With the -l option, aspell runs in list mode: Input comes from standard input, and aspell displays each potentially misspelled word on standard output. The following command produces a list of possible misspellings in the file letter.txt:

```
$ aspell -l < letter.txt
```

The next shell script, spell_check, shows another use of a while structure. To find the incorrect spellings in a file, you can use spell_check, which uses aspell to check your file against a system dictionary but goes a step further: It enables you to specify your own list of correct words and removes these words from the output of aspell. This script is useful for removing words that you use frequently, such as names and technical terms, that are not in a standard dictionary.

Although you can duplicate the functionality of spell_check using aspell, spell_check is included here for its instructive value.

The spell_check script requires two filename arguments: the list of correctly spelled words, and the second file is the one you want to check. The first statement verifies that the user specified two arguments, and the next two if statements verify that both arguments are readable files. (The exclamation point negates the sense of the following operator; the -r operator causes test to determine whether a file is readable. The result is a test that determines whether a file is not readable.)