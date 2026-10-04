# Chapter 4. Tcl Code Examples

An atom may be:

| Definition | Example | Description |
|---|---|---|n| A single character | x | Will match the character x |
| A range of characters enclosed in brackets | [a-q] | Will match any lowercase letter between a and q (inclusive) |
| A period | . | Will match any character |
| A caret | ^ | Matches the beginning of a string |
| A dollar sign | $ | Matches the end of a string |
| A backslash sequence | \^ | Inhibits treating *, &, $, +, ^, etc. as special characters and matches the exact character |

A regular expression enclosed in parentheses ([Tt]c1) Will match that regular expression

+   * Atoms can be combined into pieces.

A piece is an atom followed by:

| Definition | Example | Description |
|---|---|---|n| Another atom | ab | Matches if each atom matches in sequence |
| An asterisk | a* | Matches 0 or more occurrences of the preceding atom (a) |
| A plus | a+ | Matches 1 or more occurrences of the preceding atom |
| A question mark | [a-z]? | Matches 0 or 1 occurrence of the preceding atom |
| Another piece | [a-z]?[0-9] | Matches a letter followed by 0 or 1 letters, followed by a number |

+   * Pieces can be combined into a regular expression.

A regular expression may be: