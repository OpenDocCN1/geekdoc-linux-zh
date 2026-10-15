```
[ [0.1455440585876967, 0.7525092872509719,
0.30168961326498955], [0.6967960669374997, 0.8715621457012694,
0.24960628132632423], [0.891389814359208, 0.9591605275600708,
0.5240885874508074] ]
>>>
```

# 16.3.8 Strings, String Formatting Conversions, and Sequence Operations

# 16.3.8.1 Strings

Strings are a class of objects in Python that can represent text, and are basically seen in their single-quoted and double-quoted form, which are interchangeable. For example:

```
>>> 'program', "program's"
('program',"program's")
>>>
```

To format strings in an expression, you can use the % binary operator to format values as strings according to a specific format definition. On a line of code, on the left of the % operator, put in a format string that has one or more code types. On the right of the % sign, put in objects you want to substitute in for the types.

The operator (s % k) produces a formatted string, given a format string s and a collection of objects in a tuple or mapping object (dictionary). The string s may be a standard or Unicode string. The format string contains two types of objects: ordinary characters (which are left unmodified) and conversion specifiers, each of which is replaced with a formatted string representing an element of the associated tuple or mapping.

If k is a tuple, the number of conversion specifiers must exactly match the number of objects in k. If k is a mapping, each conversion specifier must be associated with a valid key name in the mapping, using parentheses. Each conversion specifier starts with the % character and ends with one of the conversion characters shown in Table 16.4.

# TABLE 16.4 String Formatting Conversions

| Character | Output Format |
|-----------|---------------|
| d, I | Decimal integer or long integer |
| u | Unsigned integer or long integer |
| o | Octal integer or long integer |
| x | Hexadecimal integer or long integer |
| X | Hexadecimal integer (uppercase letters) |
| f | Floating point as [–] m.dddddd |
| e | Floating point as [–] m.dddddd e±xx |
| E | Floating point as [–] m.dddddd E±xx |
| g, G | Use %e or %E for exponents less than –4 or greater than the precision |
| s | String or any object. The formatting code uses str() to generate strings |
| r | Produces the same string as produced by repr() |
| c | Single character |
| % | Literal % |