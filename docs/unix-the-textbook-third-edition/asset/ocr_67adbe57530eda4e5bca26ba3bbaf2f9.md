# TABLE 7.1 Regular Expression Operators and Their Support by UNIX Tools

| Name/Function | Operator | Example Usage | Meaning | Supported by |
|---|---|---|---|---|
| Alternation (OR) | | | x | y | z | x, y, or z | awk, grep |
| Any character | . | .com | Acom, acom, Bcom, bcom, Ccom, ccom, ... | All |
| Beginning of line | ^ | ^x | A line starting with x | All |
| Concatenation (AND) | None | xyz | xyz | All |
| End of line | $ | x$ | A line ending with x | All |
| Escape sequence: Cancels the special meaning of the metacharacter that follows it | \ | \* | * | ed, sed, vi |
| Delimiter: Marks the beginning or end of a regular expression | / | /L..e/ | Love, Live, Lose, Lase, ... | ed, sed, vi |
| Grouping | ( ) or \( \) | (xy)+ | xy, xxyy, xxyyxy, ... | All |
| Optional | ? | xy? | x, xy | awk, egrep |
| Repetition (0 or more times) | * | xy* | x, xy, xyy, xyyy, ... | All |
| Repetition (1 or more times) | + | xy+ | xy, xyy, xyyy, ... | awk, egrep |
| Matches any character enclosed in brackets. | [ ] | /[Hh]ello/ | Hello, hello | All |
| Matches any character not enclosed in brackets. | [^] | /[^A-KM-Z]ove/ | Love | All |

# TABLE 7.2 Examples of Regular Expressions for vim and Their Meaning

| Regular Expression | Meaning | Examples |
|---|---|---|
| /^Yes/ | A line starting with the string Yes | Yes... Yesteryear... Yesterday... and so on |
| /th/ | Occurrence of the string th anywhere in a word | the, there, path, bathing, and so on |
| /:$/ | A line ending with a colon | ... following: ... below: ... follows: and so on |
| /[0-9]/ | A single digit | 0, 1, ..., 9 |
| [a-z][0-9]/ | A single lowercase English letter followed by a single digit | a0, a1, a9, ..., b0, b1, ..., b9, ..., z0, ..., z1, ... z9 |
| /\..c/ | Any word that ends with .c (all C source code files) | lab1.c, program1.c, client.c, server.c, and so on |
| /[a-zA-Z ]*/ | Any string composed of letters (uppercase or lowercase) and spaces; no numbers and punctuation marks | All strings without numbers and punctuation marks such as Hello world |