# Chapter 3. Introduction to the Tcl Language

substr The substring to search for.

string The string to search in.

The string length command returns the number of characters in a string.

**Syntax:** string length string

string Defines this as a string command.

length Returns the number of characters in string.

string The string.

The string range command returns the characters between two points in the string.

**Syntax:** string range string first last

string Defines this as a string command.

range Returns the characters in string between first and last.

string The string.

The format command emulates the behavior of the C sprintf function. It takes as arguments a format description and a set of values that will be used to replace the % fields in the format description. A percent symbol can be generated with a % % field.

The format for the % fields is the same as that used in the C library. The field definition is a string composed of a leading percent sign, two optional fields, and a format definition:

```
$?justification ?field width format definition
```

+   * The first character in a field is a % symbol.

+   * The field justification may be a plus or minus sign. A minus sign causes the contents of the % field to be left justified. A plus sign causes the contents to be right justified.

+   * The field width is a numeric field. If it is a single integer, it defines the width of the field in characters. If this value is two integers separated by a decimal point, then the first integer represents the total width

54