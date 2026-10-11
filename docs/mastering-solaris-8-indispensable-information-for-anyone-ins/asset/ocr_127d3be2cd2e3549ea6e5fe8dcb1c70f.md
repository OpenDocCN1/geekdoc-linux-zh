history and alias built-ins. To avoid incorrect results, you should quote the exclamation points so the shell does not mistakenly interpret them.

You can create short names for often used commands. This saves a lot of time when you're programming scripts that use the same types of commands repeatedly. Numbers are allowed as aliases. If an alias is not defined, it will report nothing. If you give the alias built-in without arguments, you will get a list of all the defined aliases.

You can protect yourself from making mistakes when deleting files by using the alias mechanism. In the following example, the interactive version of rm is replaced by the command rid. The -i option causes rm to query you on each file to be deleted so that you do not accidentally delete the wrong files:

```
```
% alias rid 'rm -i'
% rid t*
rm: remove 'timetable.trn'? n
rm: remove 'tina.txt'? n
rm: remove 'tipa.mem'? n
```
```

An alias can be removed with the unalias built-in. Here is the syntax for the unalias built-in:

```
```
% unalias rid
```
```

# ## The C Shell and Command-Line Expansion

Unlike the history and alias built-in expansions, which are available only in interactive shells such as the C shell, command-line expansion is available in shell scripts. When the shell looks at a command, it first parses the command into tokens or words. It then scans each token for special characters and patterns, which might instruct the shell to take certain actions. Before executing the command, the shell will perform expansion on the tokens wherever necessary. Ambiguous characters such as [ ], *, and ? may end up with an actual filename.

Brace expansion is used to specify filenames and can be used to generate arbitrary strings as well. Comma-separated strings enclosed in braces { } are usually prepended with an optional identifier and appended with an optional suffix. Left-to-right order is preserved. Brace expansions may be nested. You can create directories with related names using brace expansion with no spaces between the braces and words. A simple example of brace expansion follows:

```
```
% echo chap_{ten,eleven,twelve}.txt
chap_ten.txt chap_eleven.txt chap_twelve.txt
```
```