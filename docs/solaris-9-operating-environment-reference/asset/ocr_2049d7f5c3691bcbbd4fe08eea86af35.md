# tbl 1383

/tmp/tar*

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | SUMwcu |
| CSI | Enabled |
| Interface Stability | Stable |

# See Also

ar(1), basename(1), cd(1), chown(1), cpio(1), csh(1), dirname(1), ls(1),\mnt(1), pax(1), setfac(1), mask(1), mknod(1M), void(1M), attributes(5),
environment(5), fsattr(5), largefile(5), mtio(7I)

# Diagnostics

Diagnostic messages are outputed for bad key characters and tape read/write errors for insufficient memory to hold the link tables.

# tbl — Format Tables for nroff or troff

# Synopsis

/usr/bin/tbl [-me] [-mm] [-ms] [filename]...

# Description

The tbl command is a preprocessor for formatting tables for nroff(1) or troff(1). A table is a rectangular arrangement of entries. Using the right commands, you can create multicolumn tables and enclose them in boxes. The tbl command automatically produces the correct column positioning. The input file names are copied to the standard output, except that lines between .TS (table start) and .TE (table end) commands are assumed to describe tables and are reformated.

If you specify no arguments, tbl reads the standard input, so you can use tbl as a filter. When you use tbl with eqn, put the tbl command first to minimize the volume of data passed through pipes.

You define the structure of a table by specifying global options, described below, as a comma-separated list on the second line of a table.

| Option | Description |
| --- | --- |
| center | Center the table on the page |
| expand | Expand the table width to the current line length |
| box | Draw a box around the entire table |
| doublebox | Draw a double-line box around the entire table |
| allbox | Enclose each cell in the table in a box |
| tab(x) | Use the character x as the data separator |