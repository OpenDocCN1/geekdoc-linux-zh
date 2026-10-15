x, y      Comma operator—evaluates x and then y
x ? y : z  Conditional expression—if x is true, y is evaluated; otherwise, z is evaluated

Except for the comma operator and conditional expression, these operators can also be used with the assignment operator, similar to the way addition (+) can be combined with assignment (=), giving +=.

# Special String Constants

Perl supports string constants that have special meaning or cannot be entered from the keyboard.

Table 23.6 shows most of the constants supported by Perl.

# TABLE 23.6 Perl Special String Constants

| Expression | Meaning |
|---|---|
| \\ | The means of including a backslash |
| \a | The alert or bell character |
| \b | Backspace |
| \cC | Control character (like holding the Ctrl key down and pressing the C character) |
| \e | Escape |
| \f | Formfeed |
| \n | Newline |
| \r | Carriage return |
| \t | Tab |
| \xNN | Indicates that NN is a hexadecimal number |
| \0NNN | Indicates that NNN is an octal (base 8) number |

# Conditional Statements: if/else and unless

Perl offers two conditional statements, if and unless, which function opposite one another. if enables you to execute a block of code only if certain conditions are met so that you can control the flow of logic through your program. Conversely, unless performs the statements when certain conditions are not met.