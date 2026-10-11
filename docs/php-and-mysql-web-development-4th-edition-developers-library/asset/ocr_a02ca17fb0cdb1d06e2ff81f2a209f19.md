# C.2.4 String Functions

Most of the functions in this section return a string result. Some of them, such as LENGTH(), take strings as arguments and return a number. For functions that operate on strings based on string positions, the position of the first (leftmost) character is 1, not 0. Several string functions are multi-byte safe: CHAR_LENGTH(), INSERT(), INSTR(), LOCATE(), LEFT(), LOCATE(), LOWER(), LTRIM(), MID(), POSITION(), REPLACE(), REVERSE(), RIGHT(), RPAD(), RTRIM(), SUBSTRING(), SUBSTRING_INDEX(), TRIM(), UCASE(), and UPPER().

+   - ASCII(str)
+     - Returns the integer value of the leftmost byte of the string str, in the range from 0 to 255. It returns 0 if str is empty or NULL if str should contain only 8-bit characters.

```
ASCII('abc')          → 97
ASCII('')             → 0
ASCII(NULL)           → NULL
```

+   - BIN(n)
+     - Returns a string containing the binary-digit representation of the argument n. The following two expressions are equivalent:

```
BIN(65)               → '1000001'
CONV(65,10,2)         → '1000001'
```

See the description of CONV() for more information.

+   - CHAR(n1, n2, ... [USING charset])
+     - Before MySQL 5.0.15, interprets the n1, n2, ... arguments as numeric character codes and returns a string in the connection character set consisting of the concatenation of the corresponding character values. The codes are interpreted modulo 256 (only the lower 8 bits are used). As of MySQL 5.0.15, character codes larger than 255 produce multiple result bytes, and the USING option may be given. Without USING, the return value is a binary string. With USING, the return value has the named character set. If the result is not legal for the character set, a warning occurs (and in strict SQL mode, the result is NULL). NULL arguments are ignored.

```
CHAR(65)              → 'A'
CHAR(97)              → 'a'
CHAR(89,105,107,101,115,33)  → 'Yikes!'
```

+   - CHAR_LENGTH(str)
+     - CHARACTER_LENGTH(str)