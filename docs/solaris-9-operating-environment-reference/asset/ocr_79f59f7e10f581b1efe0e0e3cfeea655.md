# 282

The following example displays the program execution headers for the zipinfo command.
castle$/usr/bin/dump -o /bin/zipinfo:

```
/bin/zipinfo:
***** PROGRAM EXECUTION HEADER *****
Type    Offset Vaddr Paddr
Filesz  Memsz Flags Align
6       0x34   0x10034 0
0xa0    0xa0     5      0
3       0xd4   0      0
0x11    0        4      0
1       0x10000 0
0x14a5a 0x14a5a 5      0x10000
1       0x14a5c 0x34a5c 0
0x4460 0x11858 7      0x10000
2       0x14d34 0x34d34 0
0xa8    0      7      0
```

castle%

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type Attribute Value |
| Availability SUNwtool |

# See Also

elfdump(1), nm(1), aout(4), ar(4), attributes(5)

# dumpcs — Show Codeset Table for the Current Locale

# Synopsis

```
/usr/bin/dumpcs [-0123vw]
```

# Description

dumpcs displays a list of printable characters for the user's current locale, along with their hexadecimal code values. The display device is assumed to be capable of displaying characters for a given locale. With no option, dumpcs displays the entire list of printable characters for the current locale.