# Table 4.6 GNU grep

| Format | What It Understands |
|---|---|
| grep 'pattern' filename(s) | Basic RE metacharacters (the default) |
| grep -G 'pattern' filename(s) | Same as above; the default |
| grep -E 'pattern' filename(s) | Extended RE metacharacters |
| grep -F 'pattern' filename | No RE metacharacters |
| grep -P 'pattern' filename | Interpret the pattern as a Perl RE |

# Table 4.7 The Basic Set—GNU grep's Regular Expression Metacharacters

| Metacharacter | Function | Example | What It Matches |
|---|---|---|---|
| ^ | Beginning-of-line anchor | ^love | Matches all lines beginning with love. |
| $ | End-of-line anchor | love$ | Matches all lines ending with love. |
| . | Matches one character | l..e | Matches lines containing an l, followed by two characters, followed by an e. |
| * | Matches zero or more characters | *love | Matches lines with zero or more spaces, of the preceding characters followed by the pattern love. |
| [ ] | Matches one character in the set | [Ll]ove | Matches lines containing 'love or Love. |
| [!] | Matches one character not in the set | [!A-K]ove | Matches lines not containing A through K followed by ove. |
| \< | Beginning-of-word anchor | \<love | Matches lines containing a word that begins with love. |
| \> | End-of-word anchor | love\> | Matches lines containing a word that ends with love. |
| \( ... \) | Tags matched characters | \(love\)able | Tags marked portion in a register to be remembered later as number 1. To reference later, use \1 to repeat the pattern. May use up to nine tags, starting with the first tag at the leftmost part of the pattern. For example, the pattern love is saved in register 1 to be referenced later as \1. |
| x\{m\} | Repetition of character x: m times, | o\{5\} | Matches if line has 5 occurrences of o. |
| x\{m,\} | at least m times, or | o\{5,\} | at least 5 occurrences of o, or |
| x\{m,n\} | between m and n times | o\{5,10\} | between 5 and 10 occurrences of o. |