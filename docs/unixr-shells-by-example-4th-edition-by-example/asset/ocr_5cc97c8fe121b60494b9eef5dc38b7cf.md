# EXAMPLE 6.193 (CONTINUED)

> Report bugs to bug-gnu-utils@prep.ai.mit.edu,\nwith a Cc: to arnold@gnu.ai.mit.edu

**Table 6.15**  *awk* Command-Line Options

| Options | Meaning |
|---|---|
| `-F fs`,<br>`--field-separator fs` | Specifies the input field separator, where fs is either a string or regular expression; for example, `FS=";"` or `FS="\t"`. |
| `-v var=value`,<br>`--assign var=value` | Assigns a value to a user-defined variable, var, before the awk script starts execution. Available to the BEGIN block. |
| `-f scriptfile`,<br>`--file scriptfile` | Reads awk commands from the scriptfile. |
| `-mf nnn`,<br>`-mr nnn` | Sets memory limits to the value of nnn. With `-mf` as the option, limits the maximum number of fields to nnn; with `-mr` as the option, sets the maximum number of records. Not applicable for awk. |
| `-W traditional`,<br>`-W compat`,<br>`--traditional`,<br>`--compat` | Runs in compatibility mode so that gawk behaves exactly as UNIX versions of awk. All gawk extensions are ignored. Both modes do the same thing; `--traditional` is preferred. |
| `-W copyleft`,<br>`-W copyright`,<br>`--copyleft` | Prints abbreviated version of copyright information. |
| `-W help`,<br>`-W usage`,<br>`--help`,<br>`--usage` | Prints the available awk options and a short summary of what they do. |
| `-W lint`,<br>`--lint` | Prints warnings about the use of constructs that may not be portable to traditional versions of UNIX awk. |
| `-W lint-old`,<br>`--lint-old` | Provides warnings about constructs that are not portable to the original version of UNIX implementations. |
| `-W posix`,<br>`--posix` | Turns on the compatibility mode. Does not recognize `\x` escape sequences, newlines as a field separator character if FS is assigned a single space, the function keyword `func`, operators `&&` and `||` to replace `^` and `^=`, and fflush. |
| `-W re-interval`,<br>`--re-interval` | Allows the use of interval regular expressions (see “The POSIX Character Class” on page 176); that is, the bracketed expressions such as `a{1alpha}`. |