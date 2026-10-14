⇒ To peruse a list containing all of the words from the text file book as they appear in the text, but with punctuation removed, type (all on one line):

```
$ sed 's/--//g' book | tr -s '[:blank:]' '\n' | tr -d '[:punct:]' | less [RET]
```

NOTES: If there is any whitespace before the first word in the input, this method inserts a newline character at the beginning of the output. To remove it, add tail +2 to the end of the pipeline but before you peruse or print it (see Recipe 9.2.3 [Displaying the End Part of Text], page 218).

# 12.2.2 Listing the Words in Text Sorted Alphabetically

To output a sorted list of the words of some text, use the method as described in the previous recipe and pipe the output to sort (see Recipe 13.6 [Sorting Text], page 320).

⇒ Here are two ways to use this.

+   - To peruse a list containing all of the words from the text file book with punctuation removed, sorted alphabetically, type (all on one line):

```
$ tr -s '[:blank:]' '\n' < book | tr -d '[:punct:]' | sort | less [RET]
```

+   - To peruse a list containing all of the words from the text file book sorted numerically, type:

```
$ tr -s '[:blank:]' '\n' < book | sort -n | less [RET]
```

This method is case-sensitive. To sort words regardless of case, first convert all uppercase letters to lowercase by piping to tr again before sort (see Recipe 13.4.1 [Changing Characters in Text], page 317).

⇒ To peruse a list containing all of the words from the text file book with punctuation removed, sorted alphabetically regardless of case, type (all on one line):

```
$ tr -s '[:blank:]' '\n' < book | tr -d '[:punct:]' | tr '[:upper:]' '[:lower:]' | sort | less [RET]
```

# 12.2.3 Listing Only the Unique Words in Text

To list the words in some text, omitting any multiple occurrences of a word, use the method as described in the previous recipe and pipe the output to uniq (see Recipe 13.5 [Filtering Out Duplicate Lines of Text], page 319).