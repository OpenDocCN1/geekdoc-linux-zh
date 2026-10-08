The printf statement produces output based on a notation similar to the File Format Notation used to describe file formats in this document. Output is produced as specified, with the first expression argument as the string format and subsequent expression arguments as the strings arg1, inclusive, with the following exceptions.

+   - The format is an actual character string instead of a graphical representation. Therefore, it cannot contain empty character positions. The space character in the format string, in any other context than a flag of a conversion specification, is treated as an ordinary character

+   - If the format set contains a \ character and that character appears in the format string, it is treated as an ordinary character that is copied to the output.

+   - The escape sequences beginning with a backslash character are treated as sequences of ordinary characters that are copied to the output. Note that these same sequences are interpreted literally by awk when they appear in literal strings, but are not treated specially by printf.

+   - A field or precision can be specified as the * character instead of a digit. In this case, the next argument from the expression is fetched, and its numeric value is taken as the field width or precision.

+   - The implementation does not precede or follow output from the d or u conversion specifications not specified by the format string.

+   - The implementation does not precede output from the o conversion specification with leading os not specified by the format string.

+   - For the c specification: if the argument has a numeric value, the character whose encoding is that value is output. If the value is negative or not the encoding of any character in the character set, the behavior is undefined. If the argument does not have a numeric value, the first character of the string value is output; if the string does not contain any characters, the behavior is undefined.

+   - For each conversion specification that consumes an argument, the next expression argument is evaluated. With the exception of the c conversion, the value is converted to the appropriate type for the conversion specification.

+   - If there are insufficient arguments to satisfy all the conversion specifications in the format string, the behavior is undefined.

+   - If any sequence in the format string begins with a % character but does not form a valid conversion specification, the behavior is unspecified.

Both print and printf can output at least one (LINE_MAX) bytes.

# Functions

The awk language has a variety of built-in functions: arithmetic, string, input/output, and general.

# Arithmetic Functions

The arithmetic functions, except for int, are based on the ISO C standard. The behavior is undefined in cases where the ISO C standard specifies that an error be returned or that although the grammar permits built-in functions to appear with no arguments or parentheses, unless the argument or parentheses are