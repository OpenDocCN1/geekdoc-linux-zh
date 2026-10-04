# A.1.1 Special Formats

These special formats can be used with the fmt attribute on other data types.

| Special Format | Description |
| --- | --- |
| whole-dollars | Displays a numeric value with the dollar sign. |
| dollars-and-cents | Displays a numeric value with the dollar sign and two decimal places. |
| collection-length | Returns the length of a collection of objects. |
| structured-text | Renders the value as structured text, which generates HTML from Zope structured text data. |

The examples in the table below all format the value -20. See section 4.3.1.2.

# C-Style Formats for the fmt Attribute

| Code | Description | Example | Result |
| --- | --- | --- | --- |
| d | Decimal numbers with preceding sign | fmt="%.3d" | -020 |
| e | Scientific notation | fmt="%.3e" | -2.000E+001 |
| E | Scientific notation | fmt="%.3E" | -2.000E+001 |
| f | Real decimal numbers | fmt="%.3f" | -20.000 |
| g | e or f abbreviated | fmt="%.3g" | -20 |
| G | E or F abbreviated | fmt="%.3G" | -20 |
| i | Decimal numbers with preceding sign | fmt="%.3i" | -020 |
| o | Octals without preceding sign | fmt="%.3o" | 37777777754 |
| s | Character string | fmt="%.2s" | -2 |
| u | Decimal numbers without preceding sign | fmt="%.3u" | 4294967276 |
| x | Hexadecimal numbers with lowercase letters and without preceding sign | fmt="%.3x" | fffec |
| X | Hexadecimal numbers with uppercase letters and without preceding sign | fmt="%.3X" | FFFFFEC |