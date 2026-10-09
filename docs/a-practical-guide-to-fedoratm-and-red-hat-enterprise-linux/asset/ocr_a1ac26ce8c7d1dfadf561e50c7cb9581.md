When CDPATH is not set and you specify a simple filename as an argument to `cd`, `cd` searches the working directory for a subdirectory with the same name as the argument. If the subdirectory does not exist, `cd` displays an error message. When CDPATH is set, `cd` searches for an appropriately named subdirectory in the directories in the CDPATH list. If it finds one, that directory becomes the working directory. With CDPATH set, you can use `cd` and a simple filename to change the working directory to a child of any of the directories listed in CDPATH.

The CDPATH variable takes on the value of a colon-separated list of directory pathnames (similar to the PATH variable). It is usually set in the `~/.bash_profile` startup file with a command line such as the following:

```
```
export CDPATH=\$HOME:\$HOME/literature
```
```

This command causes `cd` to search your home directory, the literature directory, and then the working directory when you give a `cd` command. If you do not include the working directory in CDPATH, `cd` searches the working directory if the search of all the other directories in CDPATH fails. If you want `cd` to search the working directory first, include a colon (:) as the first entry in CDPATH:

```
```
export CDPATH=:\$HOME:\$HOME/literature
```
```

If the argument to the `cd` builtin is anything other than a simple filename (i.e., if the argument contains a slash (/)), the shell does not consult CDPATH.

# ## KEYWORD VARIABLES: A SUMMARY

Table 9-5 lists the *bash* keyword variables.

Table 9-5    *bash* keyword variables

| Variable   | Value                                                                                       |
|------------|---------------------------------------------------------------------------------------------|
| BASH_ENV   | The pathname of the startup file for noninteractive shells (page 331)                       |
| CDPATH     | The `cd` search path (page 364)                                                            |
| COLUMNS    | The width of the display used by `select` (page 1012)                                      |
| HISTFILE   | The pathname of the file that holds the history list (default: `~/.bash_history`; page 377) |
| HISTFILESIZE | The maximum number of entries saved in HISTFILE (default: 1000; page 377)                  |
| HISTSIZE   | The maximum number of entries saved in the history list (default: 1,000; page 377)         |
| HOME       | The pathname of the user's home directory (page 358); used as the default argument for `cd` and in tilde expansion (page 182) |
| IFS        | Internal Field Separator (page 363); used for word splitting (page 411)                    |
| INPUTRC    | The pathname of the Readline startup file (default: `~/.inputrc`; page 390)                 |