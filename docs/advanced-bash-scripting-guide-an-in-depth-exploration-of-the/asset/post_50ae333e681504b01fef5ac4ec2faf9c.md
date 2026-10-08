
# Advanced Bash-Scripting Guide

```
With [Unicode support]:
erik@erik-desktop:~$ capture5 time ./cap-ngrep.sh
live2.pcap > out.txt
```

| real 0m50.232s |
| user 3m51.118s |
| sys 0m11.221s |

A large part of the overhead that is optimized is, I believe,
regex matching with [ string = REGEX ],
but it may help with other portions of the code as well.
i hadn't [seen it] mentioned that this optimization helped with Bash, but it has helped with "grep".
why not try?

Certain operators, notably expt, are very inefficient and might be replaced by double parentheses arithmetic expression. See Example A-59.

# Math tests

```
math via $(())
real 0m00.294s
user 0m00.288s
sys 0m00.008s
```

```
math via expr:
real 1m17.879s # Much slower!
user 0m03.600s
sys 0m08.765s
```

```
math via let:
real 0m00.364s
user 0m00.372s
sys 0m00.000s
```

Condition tests in scripts deserve close scrutiny. Substitute case for if-then constructs and combine tests when possible, to minimize script execution time. Again, refer to Example A-59.

```
Test using "case" construct:
real 0m00.329s
user 0m00.320s
sys 0m00.000s
```

```
Test with if [], no quotes:
real 0m00.438s
user 0m00.432s
sys 0m00.008s
```

```
Test with if [], quotes:
real 0m00.476s
user 0m00.452s
sys 0m00.024s
```

```
Test with if [], using -eq:
real 0m00.457s
user 0m00.456s
```

# Chapter 36. Miscellany

# Advanced Bash-Scripting Guide

Erik Brandsberg recommends associative arrays in preference to conventional numeric-indexed arrays in most cases. When overwriting values in a numeric array, there is a significant performance penalty vs. associative arrays. Running a test script confirms this. See Example A-60.

# Assignment tests

```
Assigning a simple variable
0m.418s
user 0m.416s
sys 0m.004s
```

```
Assigning a numeric index array entry
0m.582s
user 0m.564s
sys 0m.016s
```

```
Overwriting a numeric index array entry
0m21.931s
user 0m.21.913s
sys 0m.016s
```

```
Linear reading of numeric index array
0m.422s
user 0m.416s
sys 0m.004s
```

```
Assigning an associative array entry
0m.800s
user 0m.796s
sys 0m.004s
```

```
Overwriting an associative array entry
0m.798s
user 0m.784s
sys 0m.012s
```

```
Linear reading of an associative array entry
0m.420s
user 0m.420s
sys 0m.000s
```

```
Assigning a random number to a simple variable
0m.402s
user 0m.388s
sys 0m.016s
```

```
Assigning a numeric index array entry randomly into 64k cells
0m.12.678s
user 0m.12.649s
sys 0m.038s
```

```
Reading a sparse numeric index array entry
0m.087s
user 0m.084s
sys 0m.000s
```

```
Assigning a sparse associative array entry randomly into 64k cells
0m.698s
user 0m.696s
sys 0m.004s
```

Reading sparse associative array entry
real 0m.083s
user 0m.084s
sys 0m.000s

Use the time and times tools to profile computation-intensive commands. Rewriting time-critical code in C, or even in assembler.

Try to minimize I/O. Bash is not particularly efficient at handling files, so consider more appropriate tools for this script, such as awk or Perl.

Write your scripts in a modular and coherent fashion, so they can be reorganized and tightened as necessary. Some of the de-optimization techniques applicable to high-level languages work for scripts, but others, such as loop unrolling, are mostly irrelevant. Above all, use common sense. For an excellent demonstration of how optimization can dramatically reduce the execution time of a script, see Example 36.7.

# 36.7. Assorted Tips

- You have a problem that you want to solve by writing Bash script. Unfortunately, you don't know where to start. One method is to plunge right in and code those parts of the script that come easily, and write the hard parts as pseudo-code.

```bash
#!/bin/bash
ARGCOUNT=1 # Need as argument.

if [ $# -ne "$ARGCOUNT" ]; then
  # Can't figure out how to code this.
  echo "Usage: $0 arguments"
  exit 1
fi

exit 0
```

# Later on, substitute working code.
# Line 6 becomes:
if [ $# -ne "$ARGCOUNT" ];
# Line 12 becomes:
echo `Usage: $0`
```

For an example of using pseudo-code, to keep a record of which scripts have run during a particular session or sessions, add the following lines to each script you want to keep. This will keep a continuing record of invocation times.

```bash
# Useful variable defined and exported in ~/.bashrc
ROOT_UID=0
E_NOTROOT=1
MAXVAL=255
SUCCESS=0
FAILURE=-1
```

# 36. Miscellaneous

# Functions

```bash
Usage ()               # message.
{
if [ -z "$1" ];      # No arg passed.
    msg=""
else
    msg=$@
fi
echo "Usage: $msg"
}
```

```bash
Check_if_root ()       # Check if root running.
{
if [ -ne "$ROOT_UID" ];  # From ex39.sh example.
then
    echo "Must be root to run this."
    exit $E_NOTROOT
fi
```

```bash
CreateTemplateName ()  # Creates a unique filename.
{
    prefix=$temp          # From ex51.sh example.
    suffix=$(date +ts)
    filename=$prefix.$suffix
}
```

```bash
isalpha()           # Tests whether entire string is alphabetic.
{
    if [[ $# -eq 1 ]] && [[ "$1" =~ ^[a-zA-Z]*$ ]]; then
        return $SUCCESS
    fi
return $FAILURE
}
```

```bash
case $1 in
    *[a-zA-Z]*) return FAILURE;
    *) return SUCCESS;      # Thanks, S.C.
esac
```

```bash
abs ()                # Absolute value.
{
    E_ARGERR=-99999       # Caution: Max return value = 255.
}
```

```bash
    if [ -z "$1" ];      # Need arg passed.
then
        return $E_ARGERR      # Obvious error value returned.
fi
```

```bash
    if [ "$1" -ge 0 ]   # If non-negative.
then
        absval=$1            # stays as-is.
else
        let absval=$(( 0 - $1 )) # Otherwise, change sign.
fi
```

```bash
return $absval
}
tolower() {
    # Converts string(s) passed as argument (s)
    # to lowercase.

    if [ -z "$1" ];
    then
        # If no argument(s) passed,
        # send error message
        echo "$(null)"
        # (C-style void-pointer error message)
        # and return from function.
        return
    fi

echo "$@" | tr A-Z a-z
# Translate all passed arguments ($)

return

# Use command substitution to set a variable to function output.
# For example:
oldvar=$(tolower "$oldvar")
# A set of mixed-CaseLeTerS
# newvar="$oldvar"
# a set of mixed-case letters
# Exercise: Rewrite this function to change lowercase passed argument(s)
# to uppercase ... toupper() [easy].
}
```

Use special-purpose comment to increase clarity and legibility in scripts.

```bash
# Caution
rm -rf *.z ## The "-rf" options to "rm" are very dangerous,
### especially with wild cards.

## Line continuation.
# This is line 1
# of a multi-line comment,
# and this is the final line.

#* Note.
#o List item.

#> Another point of view.
while [ "$var" = "end" ]; # while test "$var" != "end"
```

Dotan Barak contributes template for a progress bar in a script.

# Example 36-17. A Progress Bar

```bash
#!/bin/bash
# progress-bar.sh

# Author: Dotan Barak (very minor revisions by ABS Guide author).
# Used in ABS Guide with permission (thanks!).
```
