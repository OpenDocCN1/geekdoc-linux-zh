# Character Classes

| alnum | Letters and digits |
| alpha | Letters |
| cntrl | CONTROL characters |
| digit | Digits |
| graph | Printable characters but not SPACES |
| lower | Lowercase letters |
| print | Printable characters, including SPACES |
| punct | Punctuation characters |
| space | Horizontal or vertical whitespace |
| upper | Uppercase letters |
| xdigit | Hexadecimal digits |

# Options

+   --delete -d Deletes characters that match those specified in string1. If used with the --squeeze-repeats option, both string1 and string2 must be given (see "Notes").

+   --squeeze-repeats -s Replaces multiple sequential occurrences of a character in string1 with a single occurrence of the character when you call tr with only one argument. If you use both string1 and string2, the tr utility first translates the characters in string1 to those in string2 and then reduces multiple sequential occurrences of characters in string2.

+   --complement -c Complements string1, causing tr to match all characters except in string1.

+   --help Gives a summary of how to use tr, including the special symbols you can use in string1 and string2.

# Notes

When string1 is longer than string2, the initial portion of string1 (equal in length to string2) is used in the translation. When string1 is shorter than string2, the GNU version of tr (described here) uses the last character of string1 to extend string1 to the length of