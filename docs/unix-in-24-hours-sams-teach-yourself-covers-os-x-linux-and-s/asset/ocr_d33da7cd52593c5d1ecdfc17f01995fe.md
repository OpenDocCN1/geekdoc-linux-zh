# Note

Before grep existed, Unix users would use a crude line-based editor called ed to find matching text. To search through a file with a regular expression, the user prefixed the command with global and had only the matches shown with print. Putting it all together, the operation was global/regular expression/print. This was shortened to g/re/p and eventually reinvented as grep.

You could spend the next 100 pages learning all the obscure and weird options to the grep family of commands. When you boil it down, however, you’re probably going to use only the simplest patterns and maybe a flag or two. Think of it this way: The English language contains more than 500,000 words (according to the Oxford English Dictionary), but you don’t have to learn them all to communicate effectively.

With this in mind, you’ll learn the basics of grep this hour, but you’ll pick up more insight into the program’s capabilities and options during the next few hours.

A few of the most important grep command flags are listed in Table 8.2.

| Flag | Function |
|------|----------|
| -c | List a count of matching lines only. |
| -i | Ignore the case of the letters in the pattern. |
| -l | List only the names of files that contain the specified pattern. |
| -n | Include line numbers. |
| -v | Show lines that don’t match the specified pattern. |

# TABLE 8.2 The Most Helpful grep Flags

+   1. The general form of grep is to specify the command, any flags you want to add, the pattern, and a filename:

Click here to view code image

```
$ grep bitnet testme
Mail/               bitnet.mailings-lists.Z  temp/
```

As you can see, grep easily pulled out the line in the testme file that contained the pattern bitnet.

+   2. Be aware that grep finds patterns in a case-sensitive manner:

Click here to view code image

```
$ grep owl testme
$
$ grep OWL testme
Archives/           OWL/                   keylime.pie
```

Note that OWL was not found in the first example because the pattern specified with the grep command was all lowercase, owl.