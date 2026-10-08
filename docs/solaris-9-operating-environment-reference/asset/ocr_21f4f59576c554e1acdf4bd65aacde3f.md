Display the SHT_DYNSYM symbol table used by ld.so.1 that is present in stripped dynamic executables. By default, the SHT_SYMTAB symbol table is displayed.

+   -D

Write external (global) symbol information.

+   -g

Do not display the output data.

+   -h

Distinguish between WEAK and GLOBAL symbols by appending an asterisk (*) to the key letter for WEAK symbols.

+   -l

Sort external symbols by name before they are printed.

+   -n

Print the value and size of a symbol in octal instead of decimal. (equivalent to -t).

+   -o

Produce easy-to-parse, terse output. Precede each symbol name by its value (blanks if undefined) and one of the letters:

+   A Absolute symbol.

+   B bss (uninitialized data space) symbol.

+   C COMMON symbol. New in the Solaris 9 release.

+   D Data object symbol.

+   F File symbol.

+   L Thread-Local storage symbol. New in the Solaris 9 release.

+   N Symbol has no type.

+   S Section symbol.

+   T Text symbol.

+   U Undefined.

If the symbol's binding attribute is:

+   LOCAL The key letter is lower case.

+   WEAK The key letter is upper case; if you specify the -l modifier, the uppercase key letter is followed by *.

+   GLOBAL The key letter is upper case.

+   -P Write information in a portable output format, as specified in “Standard Output” on page 988.

+   -r Prepend the name of the object file or archive to each output line.

+   -R Print the archive name (if present), followed by the object file and symbol name. If you also specify the -r option, ignore this option.

+   -s Print section name instead of section index.

+   -t format Write each numeric value in the specified format. The format depends on the single character used as the format option.

+   d Write the offset in decimal (default).

+   o Write the offset in octal.