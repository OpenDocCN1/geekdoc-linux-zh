# EXAMPLE (CONTINUED)

```
sed 's/134345/g' file
sed: Ending delimiter missing on substitution: s/134345/g
```

# EXPLANATION

+   1. The `v` command is unrecognized by sed. The exit status was 2, indicating that sed exited with a syntax problem.
+   2. The pattern `^/John` is missing the closing forward slash.
+   3. The substitution command, `s`, contains the search string but not the replacement string.

# 5.8  Metacharacters

Like grep, sed supports a number of special metacharacters to control pattern searching. See Table 5.3.

**Table 5.3**  sed’s Regular Expression Metacharacters

| Metacharacter | Function | Example | What It Matches |
|---|---|---|---|
| `^` | Beginning-of-line anchor | `/^love/` | Matches all lines beginning with love. |
| `$` | End-of-line anchor | `/love$/` | Matches all lines ending with love. |
| `.` | Matches one character, but not the newline character | `/l..e/` | Matches lines containing an l, followed by two characters, followed by an e. |
| `*` | Matches zero or more characters | `/ *love/` | Matches lines with zero or more spaces, followed by the pattern love. |
| `[ ]` | Matches one character in the set | `/[lT]love/` | Matches lines containing love or Love. |
| `[^ ]` | Matches one character not in the set | `/[^A-KM-Z]love/` | Matches lines not containing A through K or M through Z followed by ove. |
| `\(\.\)` | Saves matched characters | `s/\(love\)/able/\1/` | Tags marked portion and saves it as tag number 1. To reference later, use `\1` to reference the pattern. May use up to nine tags, starting with the first tag at the leftmost part of the pattern. For example, love is saved in register 1 and remembered in the replacement string. lovable is replaced with lover. |