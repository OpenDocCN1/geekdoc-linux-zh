# Table 13.14 bash Environment Variables (continued)

| Variable Name | Meaning |
|---|---|
| SHELL | When the shell is invoked, it scans the environment for this name. The shell gives default values to PATH, PS1, PS2, MAILCHECK, and IFS. HOME and MAIL are set by login(1). |
| SHELLOPTS | Contains a list of enabled shell options, such as braceexpand, hashall, monitor, etc. |
| SHLVL | Incremented by one each time an instance of bash is started. |
| TMOUT | Specifies number of seconds to wait for input before exiting. |
| UID | Expands to the user ID of the current user, initialized at shell startup. |

a. Not available in bash versions prior to 2.x.

# Setting Environment Variables.

To set environment variables, the export command is used either after assigning a value or when the variable is set. (See Table 13.15.) The declare built-in, given the -x option, will do the same. (Do not use the $ on a variable when exporting it.)

# FORMAT

```
export variable=value
variable=value; export variable
declare -x variable=value
```

# EXAMPLE 13.34

```
export NAME=john
PS1='\d\W\$USER\$ ' ; export PS1
declare -x TERM=sun
```

# Table 13.15 The export Command and Its Options

| Option | Value |
|---|---|
| -- | Marks the end of option processing; the remaining parameters are arguments. |
| -f | Name-value pairs are treated as functions, not variables. |
| -n | Converts a global (exported) variable to a local variable. The variable will not be exported to child processes. |
| -p | Displays all the global variables. |