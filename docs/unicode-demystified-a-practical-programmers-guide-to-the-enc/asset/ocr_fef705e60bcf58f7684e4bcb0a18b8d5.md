# Command Line Expansion 607

+   4. Variable expansion (page 610)
5. Command substitution (page 611)
6. Arithmetic expansion (page 611)
7. Word splitting (page 612)
8. Pathname expansion (page 614)

The order in which the various expansions take place is important; if the performed the expansions in a different order, a dramatically different result could occur. In the following example, if pathname expansion occurred prior to variable expansion, the asterisk (*) would not be treated specially; after expansion, the argument given to echo would be tmpe, and that would be the output of echo:

```
$ ls
tmp1 tmp2 tmp3
$ var=*
$ echo $var
tmp1 tmp2 tmp3
```

It is important to keep in mind that double and single quotation marks cause the shell to behave differently when performing expansions (page 568). Double quotation marks permit parameter and variable expansion but suppress other types of expansion. Single quotation marks suppress all types of expansion.

# Brace Expansion

Brace expansion, which originated in the original C Shell, provides a convenient way to specify filenames when pathname expansion does not apply. Although brace expansion is almost always used to specify filenames, the mechanism can be used to generate arbitrary strings; the shell does not attempt to match the brace notation with a list of the names of existing files. The following example illustrates the way that brace expansion works:

```
$ ls
$ echo chap_{one,two,three}.txt
chap_one.txt chap_two.txt chap_three.txt
```

The ls command shows that no files are in the working directory. The shell expands the comma-separated strings inside the braces into a SPACE-separated list of strings. Each string from the list is prepended with the string chap_, called the preamble, and appended with the string .txt, called the postamble. Both preamble and postamble are optional, and the left-to-right order of the strings within the braces are preserved in the expansion. For the shell to treat the left and right braces specially and