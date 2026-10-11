d1close.o:
  _ U_dl_close

The first column of output is the location (the offset in hexadecimal bytes) in the member, d1open.o, of the various symbols, which are listed in the third column of the output. The second column is a single letter that indicates each symbol's status. U means that the listed symbol is undefined in the member, although it might be defined in another file. AT indicates that the corresponding symbol is defined in the member's text (code) area. W specifies a symbol that will either be overridden if an identically named symbol is located in another file or, if a like-named symbol is not found, it will be replaced by a 0.

# The ar Command

ar creates, modifies, or extracts archives. It is most commonly used to create static libraries, which are files that contain one or more object files. Static libraries are object files whose code is designed to be linked into a program at compile-time rather than linked into a program dynamically at runtime. Static libraries are the conceptual opposite of Windows' dynamic link libraries (DLLs). The constituent object files are called members. ar also creates and maintains a table that cross-references symbol names to the members in which they are defined. An example of using the ar command is given in the section "Creating a Static Library," later in this chapter. The ar command has the following syntax:

```
ar [dmptrx] [options] [member] archive_file file [ . . . ]
```

ar creates the archive named archive_file from the files listed in file. At least one of the d, m, p, q, u, r or x options is required. You will normally use r. Table 14.2 describes the most commonly used ar options.

Table 14.2: Options for the ar Command

| Option | Description |
| :----- | :---------- |
| -c     | Creates archive if it doesn't exist and suppresses the message ar would emit if archive doesn't exist. The archive will still be created whether -c is specified or not. |
| -s     | Creates or updates the map linking symbols to the member in which they are defined. |
| -r     | Inserts file into the archive and replaces any existing member whose name matches that being added. New members are added at the end of the archive. |
| -q     | Appends files to the end of archive without checking for replacements. |