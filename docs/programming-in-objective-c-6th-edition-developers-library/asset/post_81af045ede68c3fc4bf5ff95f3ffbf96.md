
# 3. Variables, Data Types, and Arithmetic Expressions

The true power of programs you create is their manipulation of data. In order to truly take advantage of this power, you need to better understand the different data types you can use, as well as how to create and name variables. C has a rich variety of math operators that you can use to manipulate your data. In this chapter you will cover:

- The int, float, double, char, and bool data types
- Modifying data types with short, long, and long long
- The rules for naming variables
- Basic math operators and arithmetic expressions
- Type casting

## Understanding Data Types and Constants

You have already been exposed to the C basic data type int. As you will recall, a variable declared to be of type int can be used to contain integral values only—that is, values that do not contain decimal places.

The C programming language provides four other basic data types: char, double, char, and bool. A variable declared to be of type float can be used for storing floating-point numbers (values containing decimal places). The double type is the same as type float, only with roughly twice the precision. The char data type can be used to store a single character, such as the letter 'a', the digit character '6', or a semicolon (';') (more on this later). Finally, the bool data type can be used to store just the values 0 or 1. Variables of this type are used for indicating an on/off, yes/no, or true/false situation. These one-or-the-other choices are also known as binary choices.

In C, any number, single character, or character string is known as a constant. For example, the number 58 represents a constant integer value. The character string "str" is an example of a constant character string. Expressions consisting entirely of constant values are called constant expressions. So, the expression 1 is a constant expression because each of the terms of the expression is a constant value. But if i were declared to be an integer variable, the expression 1 would not represent a constant expression because its value would change based on the value of i. If i is 10, the expression is equal to 125, but if i is 200, the expression is equal to −65.

## The Integer Type int

In C, an integer constant consists of a sequence of one or more digits. A minus sign preceding the digit sequence indicates that the value is negative. The values 1, −1, and 0 are all valid examples of integer constants. No embedded spaces are permitted between the digits, and values larger than 9 cannot be expressed using commas. (So, the value 1 is not a valid integer constant and must be written as 1.)

Two special formats in C enable integer constants to be expressed in a base other than decimal (base 10). If the first digit of the integer value is a 0, the integer is taken as expressed in *octal* notation—therefore, in base 8. In that case, the remaining digits of the value must be valid base-8 digits and, therefore, must be 0–7. So, to express the value 5 in base 8 in C, which is equivalent to the value 4 in decimal, the notation 0 is used. Similarly, the octal constant 0 represents the decimal value 1 (1 × 64 + 7 × 8 + 7). An integer value can be displayed at the terminal in octal notation by using the format characters %o in the format string of a printf statement. In such a case, the value is displayed in octal without a leading zero. The format character %O does cause a leading zero to be displayed before an octal value.

If an integer constant is preceded by a zero and the letter x (either lowercase or uppercase), the value is taken as being expressed in hexadecimal (base 16) notation. Immediately following the letter x are the digits of the hexadecimal value, which can be composed of the digits 0–9 and the letters a–f (or A–F). The letters represent the values 10–15, respectively. So, to assign the hexadecimal value FF to an integer variable called r, the statement

```c
r = 0xFF;
```

can be used. The format characters %x display a value in hexadecimal format without the leading 0x, and using lowercase letters a–f for hexadecimal digits. To display the value with the leading 0x, you use the format characters %X, as in the following:

![](img/e50cb5e8cc6587186db5746e2ac19394_37_0.png)

```c
printf("%X", value);
```

An uppercase x, as in %X or %o, can be used to display the leading x and the hexadecimal digits that follow using uppercase letters.

## Storage Sizes and Ranges

Every value, whether it’s a character, integer, or floating-point number, has a *range* of values associated with it. This range has to do with the amount of storage that is allocated to store a particular type of data. In general, that amount is not defined in the language. It typically depends on the computer you’re running, and is, therefore, called *implementation-* or *machine-dependent*. For example, an integer might take up 32 bits on your computer, or perhaps it might be stored in 64. You should never write programs that make any assumptions about the size of your data types. You are, however, guaranteed that a minimum amount of storage will be set aside for each basic data type. For example, it’s guaranteed that an integer value will be stored in a minimum of 32 bits of storage, which is the size of a “word” on many computers.

## The Floating Number Type float

A variable declared to be of type float can be used for storing values containing decimal places. A floating-point constant is distinguished by the presence of a decimal point. You can omit digits before the decimal point or digits after the decimal point, but obviously you can’t omit both. The values 3.0, 1.0, and .0 are all valid examples of floating-point constants. To display a floating-point value at the terminal, the printf conversion characters %f are used.

Floating-point constants can also be expressed in *scientific notation*. The value 1.0e10 is a floating-point value expressed in this notation and represents the value 10,000,000,000. The value before the letter e is known as the *mantissa*, whereas the value that follows is called the *exponent*. This exponent, which can be preceded by an optional plus or minus sign, represents the power of 10 by which the mantissa is to be multiplied. So, in the constant 2.25e-3, the 2.25 is the value of the mantissa and -3 is the value of the exponent. This constant represents the value 2.25 × 10⁻³, or 0.00225. Incidentally, the letter e, which separates the mantissa from the exponent, can be written in either lowercase or uppercase.

To display a value in scientific notation, the format characters %e or %E should be specified in the printf format string. The printf format characters %g or %G can be used to let printf decide whether to display the floating-point value in normal floating-point notation or in scientific notation. This decision is based on the value of the exponent: If it’s less than -4 or greater than 5, %e (scientific notation) format is used; otherwise, %f format is used.

Use the %f format characters for displaying floating-point numbers—it produces the most aesthetically pleasing output.

A *hexadecimal* floating constant consists of a leading 0f or 0xF followed by one or more decimal or hexadecimal digits, followed by a p or P, followed by an optionally signed binary exponent. For example, 0x1p-1 represents the value 1 × 2⁻¹ = 0.5.

## The Extended Precision Type double

The double type is very similar to the float type, but it is used whenever the range provided by a float variable is not sufficient. Variables declared to be of type double can store roughly twice as many significant digits as can a variable of type float. Most computers represent double values using 64 bits.

Unless told otherwise, all floating-point constants are taken as double values by the C compiler. To explicitly express a float constant, append either an f or F to the end of the number, as follows:

1.0f

To display a float value, the format characters %d, %e, or %f, which are the same format characters used to display a double value, can be used.

## The Single Character Type char

A char variable can be used to store a single character.¹ A character constant is formed by enclosing the character within a pair of single quotation marks. So 'a', ';', and '0' are all valid examples of character constants. The first constant represents the letter a, the second is a semicolon, and the third is the character zero—which is not the same as the number zero. Do not confuse a character constant, which is a single character enclosed in single quotes, with a character string, which is any number of characters enclosed in double quotes.

> ¹ *Appendix A discusses methods for storing characters from extended character sets, through special escape sequences, universal characters, and wide characters.*

The character constant '\n' — the newline character—is a valid character constant even though it seems to contradict the rule cited previously. This is because the backslash character is a special character in the C system and does not actually count as a character. In other words, the C compiler treats the character '\n' as a single character, even though it is actually formed by two characters. There are other special characters that are initiated with the backslash character. Consult *Appendix A*, “C Language Summary,” for a complete list.
