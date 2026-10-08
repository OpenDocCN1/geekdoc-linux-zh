# Advanced Bash-Scripting Guide

```
# Variables PCT and PS1 can be merged into a new PS1 variable:
ps1="\if if [ \$EUID -eq 0 ]]; then PCT='$$LIGHTRED';
else PCT='$LIGHTBLUE'; fi;
echo '\n$GREEN[\w] \n$DARKGRAY('\$PCT\$DARKGRAY)-\n('\$PCT\$DARKGRAY)-('\$PCT\$DARKGRAY)$YELLOW-> NC\''\'
# The trick is to use strong quoting for parts of old PS1 variable.
```

Appendix M. Sample .bashrc and .bash_profile Files

836