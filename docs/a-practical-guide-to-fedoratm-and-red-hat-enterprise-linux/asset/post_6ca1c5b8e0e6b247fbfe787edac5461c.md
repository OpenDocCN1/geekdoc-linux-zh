
You can specify arguments when you call a function. Within the function these arguments are available as positional parameters (page 1022). The following example shows the `arg1` function entered from the keyboard:

```
$ arg1 ( { echo "$1"; })
$ arg1 first_arg
first_arg
```

See the function `switch` on page 332 for another example of a function.

**optional** The following function allows you to place variables in the environment (export them) using `tcsh` syntax. The `env` utility lists all environment variables and their values and verifies that `setenv` worked correctly:

```
$ cat .bash_profile
...
# setenv - keep tcsh users happy
setenv() {
    if [ $# -eq 2 ]
    then
        eval $1=$2
        export $1
    else
        echo "Usage: setenv NAME VALUE" 1>&2
    fi
}
$ . ~/.bash_profile
$ setenv TCL_LIBRARY /usr/local/lib/tcl
$ env | grep TCL_LIBRARY
TCL_LIBRARY=/usr/local/lib/tcl
```

The `$#` special parameter (page 1027) takes on the value of the number of command-line arguments. This function uses the `eval` builtin to force `bash` to scan the command `$1=$2` *twice*. Because `$1=$2` begins with a dollar sign ($), the shell treats the entire string as a single token—a command. With variable substitution performed, the command name becomes `TCL_LIBRARY=/usr/local/lib/tcl`, which results in an error. With `eval`, a second scanning splits the string into the three desired tokens, and the correct assignment occurs. See page 1051 for more information on `eval`.

## Controlling `bash`: Features and Options

This section explains how to control `bash` features and options using command-line options and the `set` and `shopt` builtins. The shell sets flags to indicate which options are set (on) and expands `$-` to a list of flags that are set; see page 1030 for more information.

### bash COMMAND-LINE OPTIONS

You can specify short and long command-line options. Short options consist of a hyphen followed by a letter; long options have two hyphens followed by multiple characters. Long options must appear before short options on a command line that calls *bash*. Table 9-12 lists some commonly used command-line options.

**Table 9-12** *bash* command-line options

| Option | Explanation | Syntax |
| --- | --- | --- |
| Help | Displays a usage message. | `--help` |
| No edit | Prevents users from using the Readline Library (page 386) to edit command lines in an interactive shell. | `--noediting` |
| No profile | Prevents reading these startup files (page 329): `/etc/profile`, `~/.bash_profile`, `~/.bash_login`, and `~/.profile`. | `--noProfile` |
| No rc | Prevents reading the `~/.bashrc` startup file (page 331). This option is on by default if the shell is called as `sh`. | `--norc` |
| POSIX | Runs *bash* in POSIX mode. | `--posix` |
| Version | Displays *bash* version information and exits. | `--version` |
| Login | Causes *bash* to run as though it were a login shell. | `-l` (lowercase “el”) |
| shopt | Runs a shell with the `opt` `shopt` option (next page). A `-0` (uppercase “O”) sets the option; `+0` unsets it. | `[+-]0 [opt]` |
| End of options | On the command line, signals the end of options. Subsequent tokens are treated as arguments even if they begin with a hyphen (-). | `--` |

### SHELL FEATURES

You can control the behavior of the Bourne Again Shell by turning features on and off. Different methods turn different features on and off: The *set* builtin controls one group of features, and the *shopt* builtin controls another group. You can also control many features from the command line you use to call *bash*.

**Features, options, variables, attributes?**

> **tip** To avoid confusing terminology, this book refers to the various shell behaviors that you can control as features. The *bash info* page refers to them as “options” and “values of variables controlling optional shell behavior.” In some places you might see them referred to as *attributes*.

## `set +o`: TURNS SHELL FEATURES ON AND OFF

The `set` builtin, when used with the `-o` or `+o` option, enables, disables, and lists certain `bash` features. For example, the following command turns on the `noclobber` feature (page 156):

```
$ set -o noclobber
```

You can turn this feature off (the default) by giving this command:

```
$ set +o noclobber
```

The command `set -o` without an option lists each of the features controlled by `set`, followed by its state (on or off). The command `set +o` without an option lists the same features in a form you can use as input to the shell. Table 9-13 lists `bash` features. This table does not list the `-i` option because you cannot set it. The shell sets this option when it is invoked as an interactive shell. See page 1024 for a discussion of other uses of `set`.

## `shopt`: TURNS SHELL FEATURES ON AND OFF

The `shopt` (shell option) builtin enables, disables, and lists certain `bash` features that control the behavior of the shell. For example, the following command causes `bash` to include filenames that begin with a period (.) when it expands ambiguous file references (the `-s` stands for `set`):

```
$ shopt -s dotglob
```

You can turn this feature off (the default) by giving the following command (the `-u` stands for `unset`):

```
$ shopt -u dotglob
```

The shell displays how a feature is set if you give the name of the feature as the only argument to `shopt`:

```
$ shopt dotglob
          dotglob off
```

Without any options or arguments, `shopt` lists the features it controls and their states. The command `shopt -s` without an argument lists the features controlled by `shopt` that are set or on. The command `shopt -u` lists the features that are unset or off. Table 9-13 lists `bash` features.

## Setting `set +o` features using `shopt`

> **tip** You can use `shopt` to set/unset features that are otherwise controlled by `set +o`. Use the regular `shopt` syntax using `-s` or `-u` and include the `-o` option. For example, the following command turns on the `noclobber` feature:

```
$ shopt -o -s noclobber
```

## Table 9-13 bash features

| Feature | Description | Syntax | Alternate syntax |
|---|---|---|---|
| **allexport** | Automatically places in the environment (exports) all variables and functions you create or modify after giving this command (default is off). | **set -o allexport** | **set -a** |
| **braceexpand** | Causes *bash* to perform brace expansion (default is on; page 405). | **set -o braceexpand** | **set -B** |
| **cdspell** | Corrects minor spelling errors in directory names used as arguments to *cd* (default is off). | **shopt -S cdspell** | |
| **cmdhist** | Saves all lines of a multiline command in the same history entry, adding semicolons as needed (default is on). | **shopt -S cmdhist** | |
| **dotglob** | Causes shell special characters (wildcards; page 165) in an ambiguous file reference to match a leading period in a filename. By default, special characters do not match a leading period: You must always specify the filenames `.` and `..` explicitly because no pattern ever matches them (default is off). | **shopt -S dotglob** | |
| **emacs** | Specifies *emacs* editing mode for command-line editing (default is on; page 387). | **set -o emacs** | |
| **errexit** | Causes *bash* to exit when a pipeline (page 158), which can be a simple command (page 147; not a control structure), fails (default is off). | **set -o errexit** | **set -e** |
| **execfail** | Causes a shell script to continue running when it cannot find the file that is given as an argument to *exec*. By default, a script terminates when *exec* cannot find the file that is given as its argument (default is off). | **shopt -S execfail** | |
| **expand_aliases** | Causes aliases (page 392) to be expanded (default is on for interactive shells and off for noninteractive shells). | **shopt -S expand_aliases** | |
| **hashall** | Causes *bash* to remember where commands it has found using *PATH* (page 359) are located (default is on). | **set -o hashall** | **set -h** |
