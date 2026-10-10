# egrep

```
egrep [ option ] regexp filename
```

Search the specified filename for the *regexp* (a regular expression). Unlike `grep`, `egrep` supports the extended regular expression characters: `+`, `?`, `|`, and `()`. You can specify more than one filename in a space-separated list or by using a shell pattern (see the section "Shell Patterns" in Chapter 4).

*See also* `fgrep`.

# OPTIONS

| Use This Option | To Do This |
|---|---|
| `-A n,` `--after-context=n` | Display *n* lines of trailing context after matching lines. |
| `-b,` `--byte-offset` | Display the byte offset within the input file before each line of output. |
| `-B n,` `--before-context=n` | Display *n* lines of leading context before matching lines. |
| `-c,` `--count` | Display a count of matching lines for each input file and hide normal output. |
| `-C n,` `--context n` | Display *n* lines of output context. The default is two lines. |
| `-d action,` `--directories=action` | In directory searches, perform the specified action. Valid options are **read** (use this directory), **recurse** (same as `-r`), or **skip**. |
| `-e regexp,` `--regexp=regexp` | Use *regexp* (regular expression). This option is provided in case you need to perform a search that begins with a hyphen. |
| `-F,` `--fixed-strings` | Force `grep` to behave like `fgrep` (searches using standard regular expressions). |