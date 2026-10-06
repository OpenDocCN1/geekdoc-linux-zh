# Advanced Bash–Scripting Guide

echo ${*:2:3} # Echoes three positional parameters, starting at second.
expr substr $string $position

Extracts length characters from $string starting at $position.

```
stringZ=abc123ABCabc
# 123456789....
# 1-based indexing.

echo expr substr $stringZ 1 2' # ab
echo expr substr $stringZ 4 3' # ABC
```

Extracts $string at beginning of $string, where $string is a regular expression.

expr "String" : \$substring\}

Extracts $string at beginning of $string, where $string is a regular expression.

```
stringZ=abc123ABCabc
echo expr match "$String" '\.([b-c]*[A-Z]..[0-9])'' # abcABC1
echo expr "$String" : '\.([b-c]*[A-Z]\.[0-9])' # abcABC1
# Both of the above forms are equivalent
```

# Substring Removal

${$substring}

Strips shortest match of $substring from front of $string.

${string#substring}

Strips longest match of $substring from front of $string.

```
stringZ=abc123ABCabc
#
#-----
#
echo ${stringZ#*aC'} 
# Strip out shortest match between 'a' and 'C'
echo ${stringZ##*a*} # abc
# Strip out longest match between 'a' and 'C'
```

${string##$substring}

Strips longest match of $substring from back of $string.

${string%%$substring}

Strips longest match of $substring from back of $string.

```
stringZ=abc123ABCabc
#
#-----
#
```

# 9.2. Manipulating Strings