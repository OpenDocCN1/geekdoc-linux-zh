string as a single token—a command. With variable substitution performed, the command name becomes `TCL_LIBRARY=/usr/local/lib/tcl`, which results in an error. Using `eval`, a second scanning splits the string into the three desired tokens, and the correct assignment occurs.

# Controlling bash: Features and Options

This section explains how to control `bash` features and options using command-line options and the `set` and `shopt` builtins.

# Command-Line Options

Two kinds of command-line options are available: short and long. Short options consist of a hyphen followed by a letter; long options have two hyphens followed by multiple characters. Long options must appear before short options on a command line that calls `bash`. Table 9-12 lists some commonly used command-line options.

**Table 9-12 Command-line options**

| **Option** | **Explanation** | **Syntax** |
| :--- | :--- | :--- |
| Help | Displays a usage message. | `--help` |
| No edit | Prevents users from using the Readline Library (page 340) to edit command lines in an interactive shell. | `--noediting` |
| No profile | Prevents reading these startup files (page 293): `/etc/profile`, `~/.bash_profile`, `~/.bash_login`, and `~/.profile`. | `--noprofile` |
| No rc | Prevents reading the `~/.bashrc` startup file (page 294). This option is on by default if the shell is called as `sh`. | `--norc` |
| POSIX | Runs `bash` in POSIX mode. | `--posix` |
| Version | Displays `bash` version information and exits. | `--version` |
| Login | Causes `bash` to run as though it were a login shell. | `-l` (lowercase "l") |
| shopt | Runs a shell with the _opt_ _shopt_ option (next page). A-`0` (uppercase "O") sets the option; `+0` unsets it. | `[±] 0` [_opt_] |
| End of options | On the command line, signals the end of options. Subsequent tokens are treated as arguments even if they begin with a hyphen (-). | `--` |


# Shell Features

You can control the behavior of the Borne Again Shell by turning features on and off. Different features use different methods to turn features on and off. The `set`