# od

Dumps the contents of a file

od [options] [file-list]

The od (octal dump) utility dumps the contents of a file, which is useful for viewing executable (object) files and text files with embedded nonprinting characters.
This utility takes its input from the file you specify on the command line or standard input.

# Arguments

The file-list includes the pathnames of the files that od displays. When you do not specify a file-list, od reads from standard input.

# Options

+   --address-radix=base
A base Specifies the base used when displaying the offsets shown for positions in the file. By default, offsets are given in octal. The values for base are d (decimal), o (octal), x (hexadecimal), and n (no offsets printed).
--format=type t type Determines the output format to use when displaying data from the file. You can repeat this option with different format types to see the file in several different formats. The possible values for type are
- Named character. Nonprinting control characters are displayed using their official ASCII names. For example, FORMFEED is displayed as ff.
- ASCII character.
- d Signed decimal.
- f Floating point.
- o Octal (default).
- u Unsigned decimal.
- x Hexadecimal.

The od utility displays certain nonprinting characters as printing characters preceded by a backslash (Table III-22). It displays nonprinting characters that are not in the file as three-digit octal numbers.