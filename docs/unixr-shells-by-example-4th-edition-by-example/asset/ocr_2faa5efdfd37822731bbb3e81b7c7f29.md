The complete command is followed by the cd command and what is called the completion rule. The p stands for the word position in the command line. The command, cd, is position 0 and its first argument is position 1. The pattern part of the rule is enclosed in slashes (p/1/) means position 1, the first argument to cd, and will be affected by the completion rule. The d part of the pattern is called a word type. See Table 9.17 on page 487 for a complete list of word types. The d word type means that only directories are to be affected by the completion. A filename or alias, for example, would not be completed if given as the first argument to cd. The rule states that whenever Tab completion is performed on the cd command, it will only take place if the first argument is a directory, and Ctrl-D will only list directories if the match is ambiguous; that is, there is more than one possible completion. See Example 9.90 for p-type completions.

# EXAMPLE 9.90

```
# p-type completions (positional completion)

1 > complete
  alias 'p/1/a/'
  cd 'p/1/d/'
  ftp 'p/1/ (owl ftp.funet.fi prep.ai.mit.edu )' 
  man 'p/1/c/'

2 > complete vi 'p/s/t/'
3 > complete vi
  vi 'p/*/t/'

4 > set autolist
5 > man fin[tab]  # Completes command names
  find fin2perl findaffix findsmb finger
6 > vi b[tab]  # Completes only filenames, not directories
  bashtest binded bindings bindit
7 > vi na[tab]mes
8 > cd sh[tab](solutions/
9 > set hosts = ( netcom.com 192.100.1.10 192.0.0.200 )
10 > complete telnet 'p/1/shosts/'
  > telnet net[tab].com
  telnet netcom.com
11 > alias m[tab]  # Completes alias names
  mc mroe mv
12
13 > ftp prep[tab]
```

# EXPLANATION

+   1 The complete built-in command, without arguments, lists all programmed completions. The following examples (lines 2 through 11) use these completion rules.
+   2 This rule states that if Tab completion is used when typing arguments to the vi command, that all arguments (*), must be of type "t" (i.e., plain text files) for completion to be performed.