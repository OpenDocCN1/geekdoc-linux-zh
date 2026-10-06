# Advanced Bash-Scripting Guide

```
case "$1" in
") echo "Usage: $0* <filename>"; exit 65; # No command-line parameters,
  # or first parameter empty.
# Note that $0#*) is ${var#pattern} param substitution. Net result is $0.

-*) FILENAME=$1;
  # If filename passed as argument ($1) starts with a dash,
  # replace it with /$1
  # so further commands don't interpret it as an option.

*) FILENAME=$1;
  # Otherwise, $1.
esac
```

# Example 10-25. Using common substitution to generate the case variable

```
#!/bin/bash
# Using command substitution to generate a "case" variable

case $(arch) in
"arch") returns machine architecture.
i386 echo "386-based machine";
i486 echo "486-based machine";
i586 echo "Pentium-based machine";
i686 echo "Pentium2+-based machine";
*) echo "Other type of machine";
esac

exit 0
```

A case construct can filter strings for globbing.

# Example 10-26. Simple string matching

```
#!/bin/bash
# match-string.sh: simple string matching

match_string ()
{
MATCH=0
NOMATCH=2
PARAMS=$2 # Function requires 2 arguments
BAD_PARAMS=$1

  [ $# -eq $PARAMS ] || return $BAD_PARAMS

  case "$1" in
  "$2") return $MATCH;
  *) return $NOMATCH;
  esac
}

a=one
b=two
c=three
d=two

match_string $a # wrong number of parameters
echo $? # 91
```

# 10.4. Testing and Branching