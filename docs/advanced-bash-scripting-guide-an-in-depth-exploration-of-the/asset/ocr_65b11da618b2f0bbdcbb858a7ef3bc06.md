# Advanced Bash-Scripting Guide

gives the backslash \ literal meaning

```
echo "\\" # Results in \

# Whereas . . 
echo "\" # Invokes secondary prompt from the command-line.
# In a script
```

The behavior of depends on whether it is escaped, strong-quoted, weak-quoted, or appearing within command substitution or a here document

```
echo lz # Simple escaping and quoting
echo \z # z
echo '\z' # z
echo "\z" # \\
echo "\\z" # z
echo "\\\\z" #
```

```
echo 'echo z' # Command substitution
echo "echo z" # z
echo 'echo \z' # z
echo "echo \\\z" # z
echo 'echo \\\\\z' # \\
echo "echo \\\\\z" # z
echo "echo \\\\\z" #
```

# Here document

```
cat <<EOF
\z
EOF # \z
```

```
cat <<EOF
\z
EOF # \z
```

# These examples supplied by Stéphane Chazelas.

Elements of a string assigned to a variable may be escaped, the escape character alone may not be assigned to a variable.

```
variable=
echo "$variable" # not work gives an error message:
# test.sh: command not found
# A "naked" escape cannot be assigned to a variable.

# What actually happens is here that the "\" escapes the newline and
++ the effect is variable=echo="$variable"
#+ invalid variable assignment
```

```
variable=
23skidoo
```

# Chapter 5. Quoting