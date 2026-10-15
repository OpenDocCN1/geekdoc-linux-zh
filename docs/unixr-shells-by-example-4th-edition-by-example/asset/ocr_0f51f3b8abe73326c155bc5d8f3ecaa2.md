# 3.1.2 Regular Expression Metacharacters

Metacharacters are characters that represent something other than themselves. The two types of metacharacters that you will learn about in this book are shell metacharacters and regular expression metacharacters. They serve different purposes. Shell metacharacters are evaluated by the UNIX/Linux shell. For example, when you use the command: rm *, the asterisk is a shell metacharacter, called a wildcard, and is evaluated by the shell to mean "Match on all filenames in the current working directory." The shell metacharacters are described for the shells in their respective chapters.

Regular expression metacharacters are evaluated by the programs that perform pattern matching, such as vi, grep, sed, and awk.2 They are special characters that allow you to delimit a pattern in some way so that you can control what substitutions will take place. There are metacharacters to anchor a word to the beginning or end of a line. There are metacharacters that allow you to specify any characters, or some number of characters, to find both upper- and lowercase characters, digits only, and so forth. For example, to change the name Tom or Tom to David, the following vi command would have done the job:

```
:1,$s/\[<T]om\>/David/g
```

This command reads, "From the first line to the last line of the file (1,$), substitute (s) the word Tom or tom with David," and the g flag says to do this globally (i.e., make the substitution if it occurs more than once on the same line). The regular expression metacharacters are \< and \> for beginning and end of a word, and the pair of brackets, [T t], match for one of the characters enclosed within them (in this case, for either T or t). There are five basic metacharacters that all UNIX/Linux pattern-matching utilities recognize. Table 3.1 presents regular expression metacharacters that can be used in all versions of vi, ex, grep, egrep, sed, and awk. Additional metacharacters are described for each of the utilities where applicable.

# Table 3.1 Regular Expression Metacharacters

| Metacharacter | Function | Example | What It Matches |
|---|---|---|---|
| ^ | Beginning-of-line anchor | /^love/ | Matches all lines beginning with love |
| $ | End-of-line anchor | /love$/ | Matches all lines ending with love |
| . | Matches one character | /l..e/ | Matches lines containing an l, followed by two characters, followed by an e |
| * | Matches zero or more of the preceding characters | /* love/ | Matches lines with zero or more spaces, followed by the pattern love |

> 2. The Korn and Bash shells now support pattern-matching metacharacters similar to the regular expression metacharacters described for grep, sed, and awk.