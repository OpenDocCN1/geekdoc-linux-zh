# Brace Expansion

The fifth step of parsing the command line is brace expansion. Brace expansion can work in two ways (it is not part of filename generation [globbing]); the first is to expand a pair of braces with a comma-separated list within:

```
zsh % echo b{a,e,i,o,u}
bat bet bit bot
```

The second way brace expansion works

```
zsh % echo {1001..1010}
1001 1002 1003 1004 1005 1006 1007 1008 1009 1010
zsh % echo {15..01}
15 14 13 12 11 10 09 08 07 06 05 04 03 02 01
```

# Filename Expansion

Filename expansion takes care of expanding tildes (~) on the command line (page 609). The Z Shell tilde (~) expansion replaces a ~ by itself command line with your home directory (HOME) and replaces a ~ followed by a user's login name with the home directory of that. Tildes are used in directory stack manipulation (page 557). ~+ is a synonym for PWD, and ~~ is a synonym for OLDPWD.

The Shell allows you to assign directory names to variables and use a tilde to refer to the directory name:

```
zsh % xbin=~/usr/bin/X11
zsh % echo ~xbin
/usr/bin/X11
```

Any other token that starts with a tilde (~) is left unchanged.

If a word in a command line begins with an equal sign, that word is checked to whether it is a command or an alias. If it is a command, the word and equal sign are replaced by the full pathname of the command. If it is an alias, it is replaced by the text of the alias. If the word is both a command and an alias, the pathname of the command is used:

```
zsh % echo =ls
/usr/bin/ls
```

# Filename Generation (Globbing)

If you not set the NO_GLOB option, the shell uses patterns to generate names for use as arguments to the command (page 754). If no filenames match the pattern, the Z Shell displays an error message unless you set the NULL_GLOB option. In that case the shell removes the unmatched pattern from the command line and continues processing. A period that either starts a pathname or follows a slash (/) in a pathname must be matched explicitly unless you set the GLOB_DOTS option.