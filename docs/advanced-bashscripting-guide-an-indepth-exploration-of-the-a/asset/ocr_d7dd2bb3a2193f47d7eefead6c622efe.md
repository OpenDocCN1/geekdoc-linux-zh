# Advanced Bash–Scripting Guide

Sed uses the -e option to specify that the following string is an instruction or set of instructions. If there is only a single instruction contained in the string, then this option may be omitted.

```
sed -n '/xzy/p' $filename
# The -n option tells sed to print only those lines matching the pattern.
# Otherwise all input lines would print.
# The -e option not necessary here since there is only a single editing instruction.
```

# Table B–2. Examples

| Notation | Effect |
|---|---|
| 8d | Delete 8th line of input. |
| /^$/ | Delete all blank lines. |
| 1,/ | Delete from beginning of input up to, and including first blank line. |
| /Jones/p | Print only lines containing "Jones" with (-n option). |
| s/Windows/Linux/ | Substitute "Linux" for first instance of "Windows" found in each input line. |
| s/BSOD/stability/g | Substitute "stability" for every instance of "BSOD" found in each input line. |
| s/ */ | Delete all spaces at the end of every line. |
| s/00*/0g | Compress all consecutive sequences of zeroes into a single zero. |
| /GUI/d | Delete all lines containing "GUI". |
| s/GUI// | Delete all instances of "GUI", leaving the remainder of each line intact. |

Substituting a zero–length string for another is equivalent to deleting that string within a line of input. This leaves the remainder of the line intact. Applying s/GUI// to the line

> The most important parts of any application are its GUI and sound effects results in
The most important parts of any application are its and sound effects

The backslash represents a newline as a substitution character. In this special case, the replacement expression continues on the next line.

```
s/^ *//g
This substitution replaces–beginning spaces with a newline. The net result is to replace paragraph indents with a blank line between paragraphs.
```

Appendix B. A Sed and Awk Micro–Primer