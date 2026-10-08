# Advanced Bash-Scripting Guide

```
function ii() {
  # Get current host related info.
  echo -e "\nYou are logged on \${Bred}\$HOST"
  echo -e "\n${Bred}Additional information:$NC " ; uname -a
  echo -e "\n${Bred}Users logged on:$NC " ; w -hs |
    cut -d ' ' -f1 | sort |
  echo -e "\n${Bred}Current date :NC " ; date
  echo -e "\n${Bred}Machine uptime :NC " ; uptime
  echo -e "\n${Bred}Memory stats :NC " ; free
  echo -e "\n${Bred}Diskspace :NC " ; mydff /HOME
  echo -e "\n${Bred}Local IP Address :NC " ; my_ip
  echo -e "\n${Bred}Open connections :NC " ; netstat -pan --inet;
}
```

```
############################################################
# Misc utilities:
###########################################################
```

```
function repeat() {
  # Repeat n times.
  local i
  max=$1;
  for ((i=1; i<= max; i++)); do # --> C-like syntax
    echo "$2"
  done
}
```

```
function ask() {
  # See 'killps' for example of use.
  echo -n "$@ " [y/n] ' ; read ans
  case $ans in
    [Y]*) return 0;
    *) return 1;
  esac
}
```

```
function corename() {
  # Get name of app that created a corefile.
  for file; do
    echo -n $file : gdb --core=$file --batch | head -1
  done
}
```

```
############################################################
###########################################################
```

PROGRAMMABLE COMPLETION SECTION
# Most are taken from the bash 2.05 documentation and from Ian McDonald's
# 'Bash completion' package (http://www.caliban.org/bash/#completion)
You will in fact need more than recent 3.0 for some features.

Note that most linux distributions provide many completions
# 'out of the box' - however, you might need to make your own one day,
# I kept those there as examples.

```
############################################################
###########################################################
```

```
if [ "${BASH_VERSION.*}" < "3.0" ]; then
  echo "You will need to upgrade to version 3.0 for full \
```

Appendix M. Sample .bashrc and .bash_profile Files