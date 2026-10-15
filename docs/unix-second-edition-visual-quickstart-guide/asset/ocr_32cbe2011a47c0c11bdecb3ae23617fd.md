# Tips

+   - "Regular expression" is often abbreviated as "regexp" in Unix documentation and Internet discussions.
+   - The command egrep is closely related to grep, adding a little more flexibility for extended regular expressions, but it fundamentally works the same. On many systems the grep command is really egrep—when you type in either one, you're really running egrep.
+   - If you're searching for whole words through large files, use fgrep for faster searching. It uses the same general syntax as grep, but searches only for whole words (not regular expressions) so goes much faster.
+   - See Chapter 1 for details about wildcards.

# Table 6.1

# Regular Expressions, Examples, and Explanations

| REGULAR EXPRESSION | FUNCTION | EXAMPLE | EXPLANATION |
|---|---|---|---|
| . | Matches any character | b.*rry | This finds all instances of "berry" or "barry." |
| * | Matches zero or more instances of the preceding item, so a*b would find "b" as well as "ab" and "aaab," but not "acb" | grep "s*day" /home/ejr/schedule | Here, the * matches zero or more of the items that immediately precede the *. |
| ^ | Matches only instances of the string at the beginning of a line | grep "^Some" sayings | With the ^, you specify that the search string must appear at the beginning of a line. The example would find a line beginning with "Some" but not one beginning with "Read Some." |
| $ | Matches only instances of the string at the end of a line | grep "ach$" sayings | With grep ach$ sayings, you could find all lines in the file sayings that end with "ach." |
| \ | Escapes (quotes) the following character—so you can search for literal characters like * or $ that are also operators | grep "\*" sayings | grep "* sayings searches for all instances of * in the sayings file. The \ tells grep to interpret the * literally, as an asterisk character, rather than as a wildcard. |
| [ ] | Matches any member of the set, like [a-z], [0-6], or [321] (three or two or one) | grep "number[0-9]" specifications | Use square brackets ([ ]) to enclose a set of options. Here, number[0-9] would match all instances of number 1, number 2, number 3, and so forth in the file called specifications. |