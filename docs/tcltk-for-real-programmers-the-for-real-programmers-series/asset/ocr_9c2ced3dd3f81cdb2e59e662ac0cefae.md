# 3.2 Data Types

# 3.2 Data Types

The primitive data type in Tcl is the string, and the composite data types are the list and the associative array. Certain complex objects such as graphic objects, I/O channels, and sockets are accessed via handles. These will be introduced briefly here, with more discussion in the following chapters.

Unlike C, C++, or Java, Tcl is a typeless language. However, certain commands can define what sort of string data they will accept. Thus, the expr command, which performs math operations, will generate an error if you try to add 5 to the string "You can't do that".

# 3.2.1 Strings

All Tcl data are strings. A string can hold alphanumeric or pure numeric data. Numeric data can be represented in Tcl as integers, floating-point values (with a decimal point), or in scientific notation. The command that receives a string will determine whether the data should be interpreted as numeric or alphabetic.

Example 3.2.1-1

LegitimateStrings

```
set alpha "abcdef"
Assign the string "abcdef" to the variable alpha.
```

```
set validString "this is a valid string"
Assign the string "this is a valid string" to the variable validString.
```

```
set number 1.234
Assign the number "1.234" to the variable number.
```

```
set scientificNotation 10e2
Assign the number "100" to the variable scientificNotation.
```