
![](img/6d8286a85e2d8ad63e16f1801102da59_334_0.png)

Figure 9-1: Output of example1.p

The print statements each have a single argument, which is displayed on the screen. The first print statement displays the string, “This is simple.” The \n characters display a new-line, which advances the cursor to the beginning of the next line. The second print statement is similar to the first. It displays the string, “Perl program,” and then advances the cursor to the beginning of the next line. Notice that the two print statements end with a semicolon. All complete statements in Perl end with a semicolon.

Note: The parentheses surrounding the print statement’s argument are optional. For example, these two statements perform the same operation:

```perl
print ( "Hello" );
print "Hello";
```

Look at the next program, which uses a variable.

```perl
#! /usr/bin/perl
# Program name: example2.p
$name = "Charlie";
print("Greetings $name\n");
```

Figure 9-2 shows the program’s output.

![](img/6d8286a85e2d8ad63e16f1801102da59_335_0.png)

The example2.p program uses the variable $name. The variable is initialized with the string “Charlie.” Notice that when $name is inserted in the print statement’s argument, it displays the contents of the variable.

Perl can also read input from the keyboard. The next program is an example.

```perl
#!/usr/bin/perl
# Program name: example3.p
print ("Enter a number: ");
$number = <STDIN>;
print ("You entered $number\n");
```

The program’s output is shown in Figure 9-3.

In Perl, <STDIN> reads input from the keyboard. The program uses this line to assign keyboard input to the variable $number:

```perl
$number = <STDIN>
```

![](img/6d8286a85e2d8ad63e16f1801102da59_336_0.png)

Figure 9-3: Output of example3.p

Like other languages, Perl offers the if-else statement as a decision structure. Here is an example:

```perl
#!/usr/bin/perl
# Program name: example4.p
print ("Enter a number: ");
$number = <STDIN>;
if ($number == 10)
{
    print ("That is the number I was thinking of.\n");
}
else
{
    print ("You entered $number\n");
}
```

The == operator tests two numeric values for equality. The if statement uses the == operator to determine if $number is equal to 10. If it is, the block (which consists of lines of code enclosed inside a set of curly braces) immediately following the if statement is executed. Otherwise, the block that follows the else statement is executed. Figure 9-4 shows the output of the program when the user enters 10.

![](img/6d8286a85e2d8ad63e16f1801102da59_337_0.png)

Figure 9-4: Output of example4.p when you enter 10

Figure 9-5 shows the output of the program when the user enters a value other than 10.

![](img/6d8286a85e2d8ad63e16f1801102da59_337_1.png)

Figure 9-5: Output of example4.p when you enter a value other than 10

Perl also has operators that test for less than, greater than, less than or equal to, and greater than or equal to relationships. Table 9-1 shows each of Perl's numeric relational operators.

| Operator | Meaning |
| :--- | :--- |
| `==` | Equality |
| `<` | Less Than |
| `>` | Greater than |
| `<=` | Less than or equal to |
| `>=` | Greater than or equal to |
| `!=` | Not equal to |

**Table 9-1: Perl's numeric relational operators**

Perl can also perform relational tests on strings, which are sequences of characters. The string relational operators, however, are different from the numeric relational operators. The next program demonstrates how two strings, stored in variables, are compared for equality.

```perl
#!/usr/bin/perl
# Program name: example5.p
$my_name = "Ellen";
$your_name = "Charlie";
if ($my_name eq $your_name)
{
    print ("Your name is the same as mine.\n");
}
else
{
    print ("Hello. My name is $my_name\n");
}
```

The eq operator tests two strings to determine if they are equal. The output of the program is shown in Figure 9-6.

![](img/6d8286a85e2d8ad63e16f1801102da59_339_0.png)

Table 9-2 lists Perl's string relational operators.

| Operator | Meaning |
| :--- | :--- |
| eq | Equality |
| lt | Less than |
| gt | Greater than |
| le | Less than or equal to |
| ge | Greater than or equal to |
| ne | Not equal to |

**Table 9-2: Perl's string relational operators**

Perl also provides standard arithmetic operators: + performs addition, - performs subtraction, * performs multiplication, and / performs division. The next program demonstrates a simple arithmetic operation.

```perl
#!/usr/bin/perl
# Program name: example6.p
$num1 = 10;
$num2 = 50;
$num3 = 12;
$average = ($num1 + $num2 + $num3) / 3;
print ("The average is $average\n");
```

Figure 9-7 shows the output of the program.

![](img/6d8286a85e2d8ad63e16f1801102da59_340_0.png)

Figure 9-7: Output of example6.p

As you can see from the program above, Perl also lets you group operations within parentheses. Now that you have a general understanding of Perl, you will study its data types.

## Identifying Data Types

The computer programmer must understand not only what is contained in files, records, and fields, but also the format in which it is stored. Are the fields of information numeric or alphabetic? Are the fields made up of a combination of numbers and letters? How do you treat control characters such as tab and new-line? Although it may seem obvious that a data item such as a person's name cannot be added or multiplied, the programmer must write code that properly handles any and all data items that appear in a program. Otherwise, misidentified data generates processing errors. To do this, programmers need to identify data types.

Data may be represented in a Perl program in a variety of ways. You will learn about these types of data:

- Variables
- Constants
- Scalars
- Arrays
- Hashes

## Variables and Constants

**Variables** are symbolic names that represent values stored in memory. For example, the variable `$x` might hold the value `100`, and `$name` might hold the sequence of characters, "Charlie." The value of a variable can change while the program runs. **Constants**, however, do not change value as the program runs. They are written into the program code itself. For example, this statement assigns the value of the constant `127.89` to the variable `$num`:

```perl
$num = 127.89
```

## Scalars

In the broadest sense, data is perceived as being either numeric or non-numeric. A non-numeric field of information is treated simply as a string of characters (hence the term *string*). Programmers associate strings with such items as a person's name, address, or license plate number. Numbers can also be used for logical analysis as well as for mathematical computations. A **scalar** is a simple variable that holds a number or a string. Scalar variable names begin with a dollar sign ($).

## Numbers

Numbers are stored inside the computer as either signed integers (as in `14321`) or double-precision floating-point values (as in `23456.85`). Numeric literals (constant values versus variable values) can be either integers or floating-point values. These numeric representations are consistent with all languages, but Perl also uses an additional convention with numeric literals to improve legibility: the underscore character, as in `5_456_678_901`. (Perl uses the comma as a list separator.) The underscore only works within literal numbers specified in a program, not in strings functioning as numbers or in data read from elsewhere. Similarly, hexadecimal constants are expressed with the leading `0x` prefix (as in `0xfff`), and octal constants are expressed with the leading `0` prefix (as in `0256`).

All of these are examples of statements that assign values to numeric scalar variables:

```perl
$x = 12;
$name = "Jill";
$pay = 12456.89;
```

## Strings

Strings are often used for logical analysis, sorts, or searches. **Strings** are sequences of any types of characters (including numbers that are treated as "characters" rather than digits). String literals are usually delimited by either single quotes (`' '`) or double quotes (`" "`). Single-quoted strings are not subject to interpolation (except for `\'` and `\\`, used to put single quotes and backslashes into a single-quoted string). Double quotes use the backslash (`\`) to precede a character that is to be treated as a control character. Table 9-3 lists the code and meaning for each string representation.
