# ## Pattern Matching

Pattern matching allows you to find patterns within the file you are editing. You can then perform functions such as changing what you have found in some way. Table 8-19 shows some of the most common pattern matching commands.

Table 8-19 Pattern Matching In vi

| Option | Action |
| :--- | :--- |
| ^ (caret) | Match the beginning of the line. To search for **Think** at only the beginning of the line, you would use: `/^Think` You can use this in combination with $, which matches to the end of the line, to delete all blank lines with: `:g/^$/d.` |
| $ | Match end of line. To match **last**. only when it is followed by a newline character, you would use: `/last.$` |
| . | Match any single character. |
| \< | Match beginning of word. |
| \> | Match end of word. |
| [string] | Match any single character in *string*. To find **mp**, **mP**, **Mp**, or **MP**, use: `/[mM][pP]` Change all occurrences of **input** or **Input** to **INPUT** with: `:%s/[Ii]nput/INPUT/g` |
| [^string] | Match any character not in *string*. |
| [a-p] | Match any character between *a* and *p*. |