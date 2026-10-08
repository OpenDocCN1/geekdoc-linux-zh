# 158

# command

-V

Write a string to standard output that indicates the name given in the `command-name` operand is interpreted by the shell in the current shell execution environment. Although the format of this string is unspecified, it indicates in which of the following categories `command-name` falls and includes the information stated below.

+   - Identify commands, regular built-in commands, and any implementation-provided functions that are found, using the PATH variable, and include the absolute path name in the string.

+   - Identify other shell functions.

+   - Identify aliases and include their definitions in the string.

+   - Identify special built-in commands.

+   - Identify regular built-in commands not associated with a PATH search.

+   - Identify shell reserved commands.

# Operands

+   argument One of the strings treated as an argument to `command-name`.

+   command-name The name of a command or a special built-in command.

# Examples

The following example makes a version of cd that always prints out the new working directory exactly once.

```
cd() {
command cd "$@" /dev/null
pwd
}
```

The following example starts a secure shell script in which the script avoids being fooled by its parent.

```
IFS='
# The preceding value should be <space><tab><newline>.
# Set IFS to its default value.
\unalias
# Set all possible aliases.
# Note that aliases is escaped to prevent an alias
# being used for aliases.
unset -f command
# Ensure command is not a user function.
PATH="$(command -p CS_PATH):$PATH"
# Put on a reliable PATH prefix.
#...
```

At this point, given correct permissions on the directories called by PATH, the script can ensure any command it calls is the intended one. The script is very