Table 14-12 (continued) 

| Option | Function |
| :--- | :--- |
| `history` | Enables command history. |
| `ignoreeof` | Ignores the `Ctrl-D` command, which normally exits the shell. |
| `noclobber` | Does not allow file redirection such as `>` to overwrite an existing file. |
| `noexec` | Reads commands but does not execute them. |
| `noglob` | Does not expand wildcards like `*` and `?`. |
| `nounset` | Reports an error when an unnamed variable is used. Normally an unnamed variable is reported as having a value of `""`. |
| `vi` | Uses the vi-style command-line editing mode. |

Another way to set shell options is with the `shopt` command, which was introduced with bash version 2. Table 14-13 lists the command-line options for `shopt`. Using the `-o` option you can use `shopt` to set those options previously set with the `set` command.

Table 14-13 
# shopt Command-Line Options 

| Option | Function |
| :--- | :--- |
| `-s` | Sets each option. |
| `-u` | Unsets each option. |
| `-q` | Suppresses normal output. Enables quiet mode. |
| `-o` | Allows the values of the option names to be those used by the `set` command. Used for backward compatibility. |
| `-p` | Displays a list of the settable options and their current values. |

A list of the most common options is shown in Table 14-14. Most options are disabled by default.