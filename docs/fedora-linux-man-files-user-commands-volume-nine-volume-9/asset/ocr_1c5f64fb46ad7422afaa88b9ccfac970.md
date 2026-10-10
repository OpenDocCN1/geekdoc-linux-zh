# DESCRIPTION

**ps2ascii** uses (1) to extract ASCII text from **PostScript**(tm) or Adobe **Portable Document Format** (PDF) files. If no files are specified on the command line, **gs** reads from standard input; but PDF input st co from an explicitly-nad file, not standard input. If no output file is specified, the ASCII text is written to standard output.

**ps2ascii** doesn’t look at font encoding, and isn’t very good at dealing with kerning, so for PostScript (but not currently PDF), you might consider **pstops** (see below).