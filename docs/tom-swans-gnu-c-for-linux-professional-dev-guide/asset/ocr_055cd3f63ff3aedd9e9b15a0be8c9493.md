effect when using the conversion character c because single characters occupy only one character space in the final output. If the conversion character is d, i, o, u, x, or X, at least the number of digits specified by the precision are output, padded at left as necessary with 0 digits.

```
% [flags] [width] [.precision] [h|l|L] conversion
```

These optional modifiers select among size-related characteristics: h (short int), l (long), or L (long double). You may use only one of the three letters. GNU C++ also recognizes a few nonstandard modifiers such as q, ll, and Z, but these are for compatibility with other systems, and you are best advised not to use them.

```
% [flags] [width] [.precision] conversion
```

The required conversion character tells sprintf() the type of an argument to be converted according to the formatting instruction. It is your responsibility to ensure that the object is of this type (however, use the GNU C++ -Wformat option to check for type mismatches). Table 8.3 lists the conversion characters you may use in formatting strings. Case is significant. A lowercase g is not the same as an uppercase G. See the info sprintf pages for more detailed descriptions and some additional quirks and rules.

# TABLE 8.3 CONVERSION CHARACTERS FOR sprintf()

| Conversion | Description |
|------------|-------------|
| % | A percent sign. |
| c | A character. |
| d | A signed decimal. |
| e | A double value to be formatted using scientific notation (for example, 1.0765e+10). |
| E | Same as e, but inserts an uppercase E before the exponent. |
| f | A double value to be formatted in decimal format such as 123.45. |
| g | A double value to be formatted in either scientific or decimal notation. The format is automatically selected to (we hope) give the most accurate results in the smallest amount of space. |
| G | Same as g, but if scientific notation is used, an uppercase E is written before the exponent. |
| i | Same as d; a signed decimal. |
| n | Treats the argument value as a pointer to an int variable in which sprintf() (and other functions in this family) stores a count of the number of characters formatted up to this point in the formatting string. Using this conversion character adds no characters to the output. It is valuable for creating variables used as column widths. |
| o | An unsigned octal. |
| p | A pointer, formatted in hexadecimal. |