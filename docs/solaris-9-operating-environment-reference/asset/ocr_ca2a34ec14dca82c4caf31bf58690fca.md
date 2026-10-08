# head 493

Eating all the gumdrops he can see
Stop, kookaburra, stop, kookaburra
Leave some there for me.
castle@

# Options

+   -n number Copy the first *number* lines of input file to standard output.
Specify the *number* option argument as a positive decimal integer.
-number Specify the *number* of lines as a positive decimal integer with the same effect as the *-n number* option.
If you specify no options, head uses a default of *-n 10.

# Operands

+   file A path name of an input file. If you specify no operands, use the standard input.

# Usage

largefile(5) for the description of the behavior of head when encountering files greater than or equal to 2 Gbytes (**=31 bytes).

# Examples

The following example writes the first 10 lines of all files (except those with a leading period) in the directory.
example@ head *

# Environment Variables

environ(5) for descriptions of the following environment variables that affect the execution of head: LC_TYPE, LC_MESSAGES, and NLPATH.

# Exit Status

+   0 Successful completion.
>0 An error occurred.

# Attributes

attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNMcu |
| CSI | Enabled |

# See Also

cat(1), more(1), pg(1), tail(1), attributes(5), environ(5), largefile(5).