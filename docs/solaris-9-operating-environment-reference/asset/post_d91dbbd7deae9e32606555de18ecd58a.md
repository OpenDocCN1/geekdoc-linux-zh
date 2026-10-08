
Expressions can contain any of the following special words.

- integer: The specified integer value. You can prefix integer values with 0i or 0I to indicate binary values, 0o prefixed with 0o or 0O to indicate octal values, 0t or 0T to indicate decimal values, and 0x or 0X to indicate hexadecimal values (the default).
- 0[tT][0-9]+\.[0-9]+
- The The specified decimal floating-point value, converted to its IEEE double-precision floating-point representation.
- cccccccc: The integer value computed by converting each character to a byte equal to its ASCII value. You can specify up to eight characters in a character constant. Characters are packed into the integer reverse order (right-to-left) beginning at the least significant byte.
- <identifier>: The value of the variable named by identifier.
- identifier: The value of the symbol named by identifier.
- (expression): The value of expression.
- .: The value of the dot.
- &: The most recent value of dot used to execute a dcmd.
- +: The value of dot incremented by the current increment.
- ^: The value of dot decremented by the current increment.

The increment is a global variable that stores the total bytes read by the last formatting dcmd. For more information on the increment, see “Formatting dcmds” on page 830.

Unary operators are right associative and have higher precedence than binary operators. The unary operators are listed below.

- #expression: Logical negation.
- -expression: Bitwise complement.
- -expression: Integer negation.
- %expression: The value of a pointer-sized quantity at the objectfile corresponding to virtual address expression in the target's virtual address space.

```
// /[csil]/expression
```
The value of a char-, short-, int-, or long-sized quantity at the objectfile location corresponding to virtual address expression in the target's virtual address space.

```
//[1248]/expression
```
The value of a 1-, 2-, 4-, or 8-byte quantity at the objectfile location corresponding to virtual address expression in the target's virtual address space.

```
*expression
```
The value of a pointer-sized quantity at virtual address expression in the target's virtual address space.

```
/*[csil]/expression
```
The value of a char-, short-, int-, or long-sized quantity at virtual address expression in the target's virtual address space.

```
/*[1248]/expression
```
The value of a 1-, 2-, 4-, or 8-byte quantity at virtual address expression in the target's virtual address space.

Binary operators are left associative and have lower precedence than unary operators. The binary operators, in order of precedence from highest to lowest, are listed below.

- Integer multiplication.
- Integer division.
- Left-hand side rounded to multiple of right-hand side.
- Integer addition.
- Integer subtraction.
- Bitwise shift left.
- Bitwise shift right.
- Logical equality.
- Logical inequality.
- Bitwise AND.
- Bitwise exclusive OR.
- Bitwise inclusive OR.

## Quoting
Each metacharacter described in "Syntax" on page 821 terminates a word unless quoted. Characters can be quoted (forcing mdb to interpret each character as itself without any special significance) by enclosure in a pair of single ('') or double (") marks. Inside double quotes, mdb recognizes C-language escape sequences.

## Variables
A variable name, a corresponding integer value, and a set of attributes variable name is a sequence of letters, digits, underscores, or periods. You can assign a value to a variable and manipulate its attributes. Each variable's value is represented as a 64-bit unsigned integer. A variable can have one or more of the following attributes:

- Read-only (cannot be modified by the user)
- Persistent (cannot be unset by the user)
- Tagged (user-defined indicator).

The following variables are defined as persistent:

- /: The most recent value.
- b: The virtual address of the base of the data section.
- d: The size of the data section in bytes.
- e: The virtual address of the entry point.
- m: The initial bytes (magic number) of the target's primary objectfile, or zero if no objectfile has been read yet.
- t: The size of the text section in bytes.
- hits: The count of the number of times the matched software specifier has measured. See "Event Callbacks" on page 834. New in Solaris 9 release.
- thread: The identifier of the current representative. The value depends on the threading model used by the target. See "Thread Support" on page 834. New in Solaris 9 release.

In addition, the mdb kernel and process export the current values of the register set as named variables. Many of these variables depend on the target name and instruction architecture.

## Symbol Name Resolution
As explained in "Syntax" on page 821, a symbol identifier present in an expression evaluates to the value of this symbol. The value typically denotes the virtual address of the storage associated with the symbol in the target's address space. A target can support multiple symbol tables including, but not limited to, a primary executable symbol, a dynamic symbol table, and standard symbol tables for each load object (such as shared libraries in a process, or kernel modules in the Solaris kernel). The target typically searches the primary executable's symbol tables, and then one or more of the other symbol tables. Notice that ELF symbol tables contain entries for every global and static symbol; automatic symbols do not appear in the symbol tables by mdb.

Additionally, mdb provides a user-defined symbol table that is searched before any of the symbol tables. The private symbol table is initially empty; it can be manipulated with :mmadd and :mmcmd. You can use the :add -P option to create symbols for program functions or data that were missing from the original or stripped out. These definitions are used when mdb converts a symbol name to an address, or an address to a symbol.

Each contains multiple tables and each can include symbols from multiple objects; different symbols with the same name can exist. mdb uses the character (*) as a symbol naming operator to enable you to obtain the value of the desired symbol in this situation. You can specify the symbol to resolve a symbol name as either *object name*, *file name*, or *object file name*. The object identifier refers to the name of a load object. The file identifier refers to the basename of a file that has a symbol of type ST_FILE in the specified symbol table. The object identifier's interpretation depends on the target type.

The mdb kernel expects object to specify the basename of a loaded kernel module. For example, the mdb name *_init evaluates the value of _init symbol in the kernel module.

The mdb process expects object to specify the name of the executable or of a shared library. It can take any of the following:

1. An exact match (that is a full path: /usr/lib/lib.so)
2. An exact name match: lib.so.1
3. An initial match up to a . suffix: lib.so or lib
4. A literal string .out is accepted as a name for the executable.

Starting in Solaris 9 release, the process target also accepts any of the four forms described above by an optional link-map ID (Lmid). The link prefix is specified by an initial LM followed by the link-map ID in hexadecimal by an additional backquote. For example, the symbol `LM0:lib.so.1 evaluates the value of the _init symbol in the lib.so.1 library that is loaded on link-map 0 (LM_ID_BASE). You may need to use the link-map specifies to resolve symbol conflicts if the same library is loaded on more than one link map.
