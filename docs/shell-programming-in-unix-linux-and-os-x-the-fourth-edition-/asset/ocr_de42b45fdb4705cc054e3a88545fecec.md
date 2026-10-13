Shell modes are turned on or off by using the -o and +o options, respectively, followed by an option name. These options are summarized in Table A.10.

Table A.10 — Shell Modes

| Mode | Meaning |
|---|---|
| `allexport` | Same as -a. |
| `errexit` | Same as -e. |
| `ignoreeof` | The exit command must be used to leave the shell. |
| `monitor` | Same as -m. |
| `noclobber` | Same as -C. |
| `noexec` | Same as -n. |
| `noglob` | Same as -f. |
| `nolog` | Don't put function definitions in the history. |
| `nounset` | Same as -u. |
| `verbose` | Same as -v. |
| `vi` | The in-line editor is set to vi. |
| `xtrace` | Same as -x. |

The command `set -o` without any options has the effect of listing all shell modes and their current settings.

The shell variable `$-` contains the current options setting.

Each word listed in `args` is set to the positional parameters $1, $2, ..., respectively. If the first word might start with a minus sign, it's safer to specify the `--` option to set to avoid interpretation of that value.

If `args` is supplied, the variable `$#` will be set to the number of parameters assigned after execution of the command.

# *Examples*

```
set -vx
set "$name" "$address" "$phone"
set -- -1
set -o vi
set +o verbose -o noclobber
```

Print all command lines as they are read, and each command and its arguments as it is executed

Set $1 to $name, $2 to $address, and $3 to $phone

Set $1 to -1

Turn on vi mode

Turn verbose mode off, noclobber on