# Table A.1 Perl Functions (continued)

| Function | Description |
| :--- | :--- |
| **pack** | `$packed=pack(TEMPLATE, LIST)`<br>Packs a list of values into a binary structure and returns the structure. `TEMPLATE` is a quoted string containing the number and type of value. `TEMPLATE` is<br>- **a** An ASCII string, null padded<br>- **A** An ASCII string, space padded<br>- **b** A bit string, low-to-high order<br>- **B** A bit string, high-to-low order<br>- **h** A hexadecimal string, low nybble first<br>- **H** A hexadecimal string, high nybble first<br>- **c** A signed char value<br>- **C** An unsigned char value<br>- **s** A signed short value<br>- **S** An unsigned short value<br>- **i** A signed integer value<br>- **I** An unsigned integer value<br>- **l** A signed long value<br>- **L** An unsigned long value<br>- **n** A short in \'network\' order<br>- **N** A long in \'network\' order<br>- **f** A single-precision float in native format<br>- **d** A double-precision float in native format<br>- **p** A pointer to a string<br>- **x** A null byte<br>- **X** Back up a byte<br>- **@** Null-fill to absolute precision<br>- **u** A uencoded string |

**package**
`package NAMESPACE`

A package declaration creates a separate namespace (symbol table) for `NAMESPACE`, the Perl way of creating a class. The `NAMESPACE` belongs to the rest of the innermost enclosing block, subroutine, `eval`, or file. If the package declaration is at the same level, the new one overrides the old one.

**pipe**
`pipe(READHANDLE, WRITEHANDLE)`

Opens a pipe for reading and writing, normally after a *fork*. See `pipe(2)`.

**pop**
`pop ARRAY`
`pop(ARRAY)`

Pops and returns the last element of the array. The array will have one less element.