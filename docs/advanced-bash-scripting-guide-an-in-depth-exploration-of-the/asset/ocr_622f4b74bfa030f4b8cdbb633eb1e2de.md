# Advanced Bash-Scripting Guide

```
awk '{if ($0 ~ /^\$cur/) print $0}'

return 0

complete -F _killall kill killps
```

```
# Local Variables:
# mode:shell-script
# sh-shell:bash
# End.
```

And, here is a snippet from Andrzej Szelachowski's instructive .bash_profile file.

# Example M-2. .bash_profile

```
# From Andrzej Szelachowski's ~/.bash_profile:

# Note that a variable may require special treatment
# if it will be exported.

DARKGRAY='\e[1;30m'
LIGHTRED='\e[1;31m'
GREEN='\e[32m'
YELLOW='\e[1;33m'
LIGHTBLUE='\e[1;34m'
NC='\e[m'

PCT="\e";if [[ $EUID -eq 0 ]]; then T=$LIGHTRED; else T=$LIGHTBLUE; fi;
echo \$T"

# For "Literal" command to be assigned to a variable,
# use escapes and double quotes:
PCT="\\\"
# Otherwise, the value of PCT variable is assigned only once,
# when the variable is exported/read from .bash_profile,
# and it will not change afterwards if the user ID changes.

PS1="="\n$GREEN[\w]$DARKGRAY($PCT%t$DARKGRAY)($PCT%u$DARKGRAY)-$PCT!$DARKGRAYYELLOW)-> \$NC"
```

+   - Escape a variable value changes:
  - if [[ $EUID -eq 0 ]];
- Otherwise the value of the EUID variable will be assigned only once,
- as above.

+   - When a variable is assigned, it should be escaped:
  - echo \$T,
- Otherwise the value of the T variable is taken from the moment the PCT
  - variable is exported/read from .bash_profile.
- So, in this example would be null.

+   - When a variable's value contains a semicolon it should be strong quoted:
  - T=$LIGHTRED";
- Otherwise, the semicolon will be interpreted as a command separator.

Appendix M. Sample .bashrc and .bash_profile Files