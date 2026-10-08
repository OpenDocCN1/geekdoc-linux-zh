# uudecode, uudecode 1499

# Operands

uudecode

decode-pathname

The path name of the file where the uudecode command puts the decoded file. If there are characters in decode-pathname that are not in the portable file-name character set, the results are unspecified.

source-file

A path name of the file to be encoded.

uudecode

encoded-file

The path name of a file containing the output of uudecode.

# Usage

See largefile(5) for the description of the behavior of uudecode and uudecode when encountering files greater than or equal to 2 Gbytes (**31** bytes).

# Environment Variables

See environ(5) for descriptions of the following environment variables that affect the execution of uudecode and uudecode: LC_CTYPE, LC_MESSAGES, and NLPATH.

# Output

The standard output is a text file (encoded in the character set of the current locale) that begins with the line

```
begin&s@s\n, <mode>, decode_pathname
```

and ends with the line

```
end\n
```

In both cases, the lines have no preceding or trailing blank characters.
The algorithm that is used for output by splitting the lines in begin and end takes six-bit intervals into four octets, containing data in the lower six bits only. These octets are converted to characters by addition of a value of 0x20 to each octet so that each octet is in the range 0x20-0x5F. It is assumed to represent a printable character. Each octet is translated into the corresponding character set for the codet used in the current locale. (For example, the octet 0x41, representing A, is translated to A in the current codet, as 0xC1 if it is EBCDIC.)

Where two octets are combined, the least significant bits of the first octet are shifted left and combined with the most significant bits of the second octet that are shifted right. The three octets A, B, C are converted into the four octets:

```
0x20 + ((A >> 2) & 0x3F)
0x20 + ((A << 4) & (B >> 4)) & 0x3F)
0x20 + ((B << 2) & (C >> 6) & 0x3F))
0x20 + ((C << 3) & 0x3F)
```

These octets are translated into the local character set.