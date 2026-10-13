| Command | Meaning |
|---|---|
| `[count]tc` | Same as `fc` followed by `h`. |
| `[count]Tc` | Same as `Fc` followed by `l`. |
| `;` | Repeats the last `f`, `F`, or `T` command. |
| `,` | Reverse of `;`. |
| `a` | Enter input mode and enter text after the current character. |
| `A` | Append text to the end of the line; same as `$`. |
| `[count]mc motion` | Delete current character through character specified by `motion` and enter input mode; if `motion` is `c`, the entire line is deleted. |
| `c` | Delete current character through end of line and enter input mode. |
| `s` | Same as `cc`. |
| `[count]d motion` | Delete current character through the character specified by `motion`; if `motion` is `d`, the entire line is deleted. |
| `D` | Delete current character through the end of line; same as `d$`. |
| `i` | Enter input mode and insert text before the current character. |
| `I` | Enter input mode and insert text before the first word on the line. |
| `[count]p` | Place the previous text modification before the cursor. |
| `[count]P` | Place the previous text modification after the cursor. |
| `[count]y motion` | Copy current character through character specified by `motion` into buffer used by `p` and `P`; if `motion` is `y`, the entire line is copied. |
| `Y` | Copy current character through the end of line; same as `y$`. |
| `R` | Enter input mode and overwrite characters on the line. |
| `[count]rc` | Replace the current character with `c`. |
| `[count]x` | Delete current character. |
| `[count]X` | Delete preceding character. |
| `[count].` | Repeat the previous text modification command. |
| `~` | Invert the case of the current character and advance the cursor. |
| `[count]_` | Append the `count` word from the previous command and enter input mode; the last word is the default. |
| *(blank)* | Attempt filename generation on the current word; if a match is found, replace the current word with the match and enter input mode. |
| `=` | List files that begin with the current word. |