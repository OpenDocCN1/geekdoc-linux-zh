# # Matching patterns

The Python “re” module can be imported into a program to make use of Regular Expression patterns that describe a particular string of characters. Regular Expressions are useful for text validation and for search-and-replace operations within text by matching their specified pattern to a section of the text.

A Regular Expression pattern may consist entirely of “literal characters” describing a character string to match within some text. For example, the Regular Expression “wind” finds a match in “*windows*” – the pattern literally matches the string in the text. More typically, a Regular Expression pattern consists of a combination of literal characters and these “metacharacters”:

| Metacharacter: | Matches: | Example: |
|---|---|---|
| . | Any Characters | py..on |
| ^ | First Characters | ^py |
| $ | Final Characters | ...on$ |
| * | Zero Or More Repetitions | py* |
| + | One Or More Repetitions | py+ |
| ? | Zero Or One Repetitions | py? |
| { } | Multiple Repetitions | a{ 3 } |
| [ ] | Character Class | [ a-z ] |
| \ | Special Sequence | \s |
| \| | Either Optional Character | a\|b |
| ( ) | Expression Group | ( ... ) |

A combination of literals and metacharacters defining a pattern to be matched can be specified to the *re.compile()* method to return a pattern object. This object has a *match()* method to specify a string within its parentheses to compare against the pattern.

When a *match()* comparison succeeds, a match object is returned containing