
## dump — Dump Selected Parts of an Object File for Shell Scripts

## Synopsis

```
/usr/ccs/bin/dump [-accfgfLlorstV] [-T index [, index]] filename...
/usr/ccs/bin/dump [-aforstl [v]] filename...
/usr/ccs/bin/dump [-hsr -d number [, numberm]] filename...
/usr/ccs/bin/dump [-hsrt [-n name]] filename...
```

## Description

The dump command dumps selected parts of its object file arguments to the standard output.
The dump command is best suited for use in shell scripts. The elfdump(1) command is recommended for more human-readable output.

## Options

The dump command accepts both object files and archives of object files. It processes each file argument according to one or more of the options listed below.

> Note - -D and -l options were removed starting with the Solaris 8 release.

- -a Dump the archive header of each member of an archive.
- -c Dump the string table(s).
- -C Dump decoded C++ symbol names.
- -f Dump each file header.
- -g Dump the global symbols in the symbol table of an archive.
- -h Dump the section headers.
- -L Dump dynamic linking information and static shared library information if available.
- -o Dump each program execution header.
- -r Dump relocation information.
- -s Dump section contents in hexadecimal.
- -t Dump symbol table entries.
- -T index
- -T index1,index2
Dump only the indexed symbol table entry defined by indexor a range of entries defined by index1, index2.
- -V Print version information.

## dump

You can use the following modifiers to modify the capabilities of the options listed above.

| Modifier | Description |
| - | - |
| -d number | Dump the number indicated by number or the range of sections starting at number1 and ending at number2. You can use this modifier with -h, -s, and -r. When you use -d with -h or -s, treat the argument as the number of a section or range of sections. When you use -d -r, treat the argument as the number of the section or range of sections to which the relocation applies. For example, to print out all relocation entries with the .text section, specify the number of the section as the argument to -d. If text is number 2 in the file, dump -d 2 prints all associated entries. To print out a specific section, use dump -s -n name for raw data output or dump -sv -n name for interpreted output |
| -n name | Dump information pertaining only to the named entity. You can use this modifier with -h, -s, -r, and -t. When you use -n with -h or -s, treat the argument as the name of a section. When you use -n with -t or -r, treat the argument as the name of a symbol. For example, dump -t -n .text dumps the symbol table associated with the symbol whose name is .text, where dump -h -n .text dumps the section header information for the .text section |
| -p | Suppress printing of headings. |
| -v | Dump information in symbolic representation instead of numeric |

- -a (date, user ID, group ID).
- -f (class, data, type, machine, version, flags).
- -h (type, flags).
- -o (type, flags).
- -r (name, type).
- -s (interpret contents wherever possible).
- -t (type, bind).
- -L (value).

When you use -v with -s, all sections that can be interpreted, such as the string table or symbol table, produces the same formatted output as dump -sv -n .symtab filename... or dump -tv filename..., but dump -s -n .symtab filename... prints raw data in hexadecimal. Without additional modifiers, dump -sv -n filename... dumps all sections in the files, interpreting all those that it can and dumping the rest (such as .text or .data) as raw data.

The dump command tries to format the information it dumps in a meaningful way, printing certain information in character, hexadecimal, octal, or decimal representation as appropriate. *dump*

## Examples

The following example shows the first few lines of the section header information for the zipinfo command.

```
castle% /usr/ccs/bin/bin/dump -h /bin/zipinfo
```

```
/bin/zipinfo:
```

| [No] | Type | Flags | Addr | Offset | Size | Name |
| --- | --- | --- | --- | --- | --- | --- |
| [1] | 1 | 2 | 0x100d4 | 0xdd4 | 0x11 | .interp |
| | | | | 0 | | |
| [2] | 5 | 2 | 0x100e8 | 0xe8 | 0x64c | .hash |
| | | | 0x4 | 0x4 | | | |
| [3] | 11 | 2 | 0x10734 | 0x734 | 0xbe0 | .dynsym |
| | | | 0x4 | 0x10 | | |
| [4] | 3 | 2 | 0x11314 | 0x1314 | 0xc25 | .dynstr |
| | | | | 0x4 | | |
| [5] | 18790490 | 2 | 0x11f3c | 0x1f3c | 0x20 | .version |
| | | | | | | | |
| 4 | 1 | | | | 0x4 | | |

For contrast, the following example shows the first few lines of output from the elfdump command.

```
castle% /usr/ccs/bin/elfdump -c /bin/zipinfo
```

```
Section Header[1]: sh_name: .interp sh_flags: [ SHF_ALLOC ]
sh_addr: 0x100d4 sh_type: [ SHT_PROGBITS ]
sh_size: 0x11 shentsize: 0
sh_offset: 0xd4 sh_info: 0
sh_link: 0
```

```
Section Header[2]: sh_name: .hash sh_flags: [ SHF_ALLOC ]
sh_addr: 0x100e8 sh_type: [ SHT_HASH ]
sh_size: 0x64c shentsize: 0x4
sh_offset: 0xe8 sh_info: 0
sh_link: 3
```

```
Section Header[3]: sh_name: .dynsym sh_flags: [ SHF_ALLOC ]
sh_addr: 0x10734 sh_type: [ SHT_DYNSYM ]
sh_size: 0xbe0 shentsize: 0x10
sh_offset: 0x734 sh_info: 28
sh_link: 4
```

The following example displays the program execution headers for zipinfo command.

```
castle% /usr/ccs/bin/dump -o /bin/zipinfo:
```

```
/bin/zipinfo:
***** EXECUTION HEADER *****
Type    Offset Vaddr Paddr
Filesz  Memsz Align
6       0x34   0x1034 0
0xa0    0xa0     5      0
3       0xd4   0      0
0x11    0        4      0
1       0x10000 0
0x14a5a 0x14a5a 5      0x1000
1       0x14a5c 0x345c 0
0x4460 0x11858 7      0x10000
2       0x14d34 0x34d4 0
0xa8    0      7      0
```

```
castle%

## Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type Attribute Value |
| --- | | |

## See Also

elfdump(1), nm(1), out(4), ar(4), attributes(5)

## dumpcs — Show Codeset Table for the Current Locale

## Synopsis

```
/usr/bin/dumpcs [-0123]
```

## Description

dumpcs displays a list of printable characters for the user's current locale, along with their hexadecimal code values. The display device is assumed to be capable of displaying characters for a given locale. With no option, dumpcs displays the entire list of printable characters for the current locale.

With one or more numeric options specified, dumpcs shows EUC charset(s) for the current locale according to the numbers specified and in order of charset number. Each nonprintable character is represented by an asterisk (*) and enough ASCII space character(s) to fill that charset's column width.

> Note — dumpcs can handle only EUC locales.

## Options

- -0 ASCII (or EUC primary) coderset.
- -1 EUCIPSET 1 if used for the current locale.
- -2 EUCIPSET 2 if used for the current locale.
- -3 EUCIPSET 3 if used for the current locale.

Verbose, ranges of nonprintable characters are collapsed into a single line. This option produces one line for each nonprintable character. Replace code values with corresponding wide character values (values).

## Examples

The following example first uses the dumpcs command with no arguments, then uses the -0 option. Notice that the output from these two commands is identical.

```
castle% dumpcs
::::::::
LC_CTYPE:C CS:0
::::::::
20  !" # $S% & ' ( ) *, . / 0 1 2 3 4 5 6 7 8 9 ; <= > =
40  @ A C D E F G H I J K L M N O P Q R S T U V W X Y Z [ ] ^ -
60  a b c d e f g h i j k l m n o p q r s u v w x y z ( | ) * -
```

```
::::::::
LC_CTYPE:C CS:1
*
20  !" # $S% & ' ( ) * +, . / 0 1 2 3 4 5 6 7 8 9 ; <= > =
40  @ A C D E F G H I J K L M N O P Q R S T U V W X Y Z [ ] ^ -
60  a b c d e f g h i j k l m n o p q r s u v w x y z ( | ) * -
```

```
castle% dumpcs -1
::::::::
LC_CTYPE:C CS:1
*
castle%
```

## Environment Variables

The environment variables LC_CTYPE and LANG control the character classification throughout dumpcs. On entry to dumpcs, these environment variables are checked in
