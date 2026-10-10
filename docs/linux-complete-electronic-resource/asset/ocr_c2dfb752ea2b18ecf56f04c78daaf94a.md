+   * **--help** Print a usage message on standard output and exit successfully.
+   * **--version** Print version information on standard output then exit successfully.

# DISPLAY COLORIZATION

When using the `--color` option, this version of `ls` will colorize the file names printed according to the name and type of file. By default, this colorization is by type only, and the codes used are ISO 6429 (ANSI) compliant.

You can override the default colors by defining the environment variable `LS_COLORS` (or `LS_CLOURS`). The format of this variable is reminiscent of the `termcap(5)` file format; a colon-separated list of expressions of the form “`xx=string`”, where xx is a two-character variable name. The variables with their associated defaults are:

| | 0 | Normal (non-filename) text |
|---|---|---|
| fi | 0 | Regular file |
| di | 32 | Directory |
| ln | 36 | Symbolic link |
| pi | 31 | Named pipe (FIFO) |
| so | 33 | Socket |
| bd | 44;37 | Block device |
| cd | 44;37 | Character device |
| ex | 35 | Executable file |
| mi | (none) | Missing file (defaults to fi) |
| or | (none) | Orphaned symbolic link (defaults to ln) |
| lc | \[e | Left code |
| rc | m | Right code |
| ec | (none) | End code (replaces lc+no+rc) |

You only need to include the variables you want to change from the default.

File names can also be colorized based on filename extension. This is specified in the `LS_COLORS` variable using the syntax “`*ext=string`”.