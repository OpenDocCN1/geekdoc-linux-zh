
# Advanced Bash-Scripting Guide

It is also possible to enable script options from the command line. Some options that will not work with set are available this way. Among these are -i, force script to run interactive.

```
bash -v script-name
```

```
bash -o verbose script-name
```

The following is a listing of some useful options. They may be specified in either abbreviated form (preceded by a single dash) or by complete name (preceded by a double dash or -o).

Table 33-1. Bash options

| Abbreviation | Name | Effect |
| --- | --- | --- |
| -B | brace expansion | Enable brace expansion (default setting = on) |
| +B | brace expansion | Disable brace expansion |
| -C | noclobber | Prevent overwriting of files by redirection (may be overridden by >i) |
| -D | (none) | List double-quoted strings by $, but do not execute commands in script |
| -a | allexport | Export all defined variables |
| -b | notify | Notify when jobs running in background terminate (or not use in a script) |
| -c ... | (none) | Read commands from ... |
| checkjobs | | Informs users of any job upon shell exit. Inherited in version 4 of Bash, and still "experimental." Usage: -s checkpoints (Caution: hang!) |
| -e | erxit | Abort at first error, when a command executes with non-zero status (except in until or while, if-tests, list constructs) |
| -f | noglob | Filename expansion (disabled) |
| globstar | globbing star-match | Enables the ** globstar (version 4+ of Bash). Usage: -s globstar |
| -i | interactive | Script runs in interactive mode |
| -n | noexec | Read commands in script, but do not execute them (syntax check) |
| -o | (none) | Invoke the Option-name |
| Option-Name | | Change the behavior of Bash, or invoked script, to conform to POSIX standard. |
| - posix | POSIX | |
| -o pipefail | pipe failure | Causes a pipeline to return the exit status of the last command in the pipe that returned a non-zero return value. |
| -p | privileged | Script runs as "sudo" (caution!) |
| -r | restricted | Script runs in restricted mode (see Chapter 22). |
| -s | stdin | Read commands from stdin |
| -t | (none) | Exit after first command |

Chapter 33. Options

# Advanced Bash-Scripting Guide

| | | |
|---|---|||
| -u | nounset | Attempt to use undefined variable outputs error message, and forces an exit |
| -v | verbose | Print each command to stdout before executing it |
| -x | xtrace | Similar to -v, but expands commands |
| - | (none) | End of options flag. All other arguments are positional parameters. |
| -- | (none) | Unset positional parameters. If arguments given (-- arg1 arg2), positional parameters set to arguments. |

# Chapter 34. Gotchas

Turandot: Gli enigmi sono tre, la morte una!

Caleph: No, no! Gli enigmi sono tre, una la vita!

--Puccini

Here are some (non-recommended!) scripting practices that will bring excitement into an otherwise dull life.

- Assigning reserved words or characters to variable names.

```bash
case=value0              # Causes problems.
23skido=valuel           # Also problems.
# Variable names starting with a digit are reserved by the shell.
# Try _23skido=value1 Starting variables with an underscore is okay.

# However .               using an underscore will not work.
=_25
echo $_               # $_ is a special variable set to last arg of last command.
# But . .               # is a valid function name!
xyz(!*=value2            # Causes severe problems.
# As of version 3 Bash, periods are not allowed within variable names.
```

- Using a hyphen or reserved characters in a variable name (or function name).

```
var-1=23
# Use 'var_1' instead.

function-whatever ()   # Error
# Use 'function_whatever' () instead.
```

# As of version 3 Bash, periods are not allowed within variable names.
function.whatever ()    # Error
# Use 'functionWhatever' () instead.

- Using the same name for a variable and a function. This can make a script difficult to understand.

```
do_something () {
  echo "This function something"
}

do_something=do_something
# All this is legal, but highly confusing.
```

- Using whitespace inappropriately. In contrast to other languages, Bash can be finicky.

```
var1 = 23 # 'var1=23' is correct.
# On line above, Bash attempts to execute "var1"
# with the arguments "=" and "23".

```
let c = $a -b  # Instead c=$a-$b  or let "c" = $a
if [ $a -le 5 ];
  if [ $a -le 5 ] is correct.
  if [ $a -le 5 ] also works.
```

Not terminating with semicolon the final command in block within brackets.

{ ls -l; echo "Done." }
# bash: syntax error: unexpected end of file

{ ls -l; echo "Done"; } # Final command needs semicolon.
```

Assuming uninitialized variables (variables before a value is assigned to) are "zeroed out". An uninitialized variable has a value of null, not zero.

```bash
#!/bin/bash
echo "initialized_var = $uninitialized_var"
# However
if $BASH_VERSION >= 4.2; then

if [[ -v uninitialized_var ]]
then
uninitialized_var=0 # Initialize it to zero!
fi
```

Mixing up -eq in a test. Remember, is for comparing literal variables and -eq for integers.

```
if [ "$a" = 273 ]; then # Is $a an integer or string?
  echo "Comparison works."
else
  echo "Comparison does not work."
fi # Comparison not work.
```

Same with a="273" and a="0273". Likewise, problems trying to use "-eq" with non-integer values.

```
if [ "$a" -eq 273.0 ]; then
  echo "a = $a"
fi # Aborts with an error message.
# test.sh: { 273.0: integer expression expected }
```

- Misusing string comparison operators.

Example 34-1. Numerical and string comparison are not equivalent

```bash
#!/bin/bash
number=1

# The following while-loop has two errors:
# one blatant, and the other subtle.

while [ "$number" < 5 ]    # Wrong! Should be: [ "$number" -lt 5 ]
do
    echo -n "$number"
    let "$number" += 1
done
```

Attempt to run this bombs with the error message:
# bad-op.sh: line 10: No such file or directory
Within single brackets, "*" must be escaped, and and even then, it's still wrong for comparing integers.

```bash
while [ "$number" \le 5 ] # 1 2 3 4
do
    echo -n "$number"      # it seems to work, but . .
    let "$number" = 1     # it actually does an ASCII comparison,
done
# better than a numerical one.
```

echo; echo "--------------------------------"
# This can cause problems. For example:

```bash
lesser=5
greater=105

if [ "$greater" \< "$lesser" ]
then
    echo "$greater is less than $lesser"
    # 105 is less than 5
    # In fact, "105" is actually less than "5"
    # in a string comparison (ASCII sort order).

echo
exit 0
```

- Attempting to let to set string variables.

```
let "a = hello, you"
echo "$a"      # 0
```

Sometimes variables within "test" brackets ([ ]) need to be quoted (double quotes). Failure to do may cause unexpected behavior. Example 7-6, Example 20-5, and Example 9-6.

- Quote a variable containing whitespace prevents splitting. Sometimes this produces unintended.

Commands from a script may fail to execute because the script owner lacks permission for them. If a user cannot invoke a command from the command-line, then piping it into a script will likewise fail.
```
