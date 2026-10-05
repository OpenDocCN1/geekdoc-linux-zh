variable speed things and save you the tedium of using cd with longer path-names to switch among them.

When CDPATH is not set and you specify a simple filename as an argument to cd, cd searches the working directory for a subdirectory with the same name as the argument. If the subdirectory does not exist, cd displays an error message. When CDPATH is set, cd searches for an appropriately named subdirectory in the directories of the CDPATH list. With CDPATH set, you can use cd and a simple filename to change the working directory to a child of any of the directories listed in CDPATH.

The CDPATH variable takes the value of a colon-separated list of directory pathnames (similar to the PATH variable). It is usually set in the ~/.bash_profile startup file by a command line such as the following:

```
export CDPATH=$HOME:$HOME/literature
```

This causes cd to search your home directory, the literature directory, and the working directory when you give a cd command. If you do not include the working directory in CDPATH, cd searches the working directory if the search of all the other directories in CDPATH fails. If you want cd to search the working directory first, include a null string, represented by two colons (;;), as the first entry in CDPATH:

```
export CDPATH=$:$HOME:$HOME/literature
```

If the argument to the cd builtin is an absolute pathname—one starting with a slash (/)—the shell does not consult CDPATH.

# KEYWORD VARIABLES: A SUMMARY

Table 9-5 presents a list of bash keyword variables.

| Variable | Value |
| --- | -- |
 BASH_ENV | The pathname of the startup file for noninteractive shells (page 294) |
| CDPATH | The cd search path (page 324) |
| COLUMNS | The width of the display used by select (page 983) |
| FCEDIT | The name of the editor that fc uses by default (page 334) |
| HISTFILE | The pathname of the file that holds the history list (default: ~/.bash_history; page 330) |
| HISTFILESIZE | The maximum number of entries saved in HISTFILE (default: 500; page 330) |
| HSTSIZE | The maximum number of entries saved in the history list (default: 500; page 330) |