
Perl statements are terminated with a semicolon. A Perl statement can extend over several actual screen lines because Perl is not concerned about whitespace.

The second line of the simple program prints the text enclosed in quotation marks. `\n` is the escape sequence for a newline character.

# TIP

Using the `perldoc` and `man` commands is an easy way to get more information about the version of Perl installed on your system. To learn how to use the `perldoc` command, enter the following:

```
$ perldoc perldoc
```

To get introductory information on Perl, you can use either of these commands:

```
$ perldoc perl
$ man perl
```

For an overview or table of contents of Perl's documentation, use the `perldoc` command like this:

```
$ perldoc perltoc
```

The documentation is extensive and well organized. Perl includes a number of standard Linux manual pages as first guides to its capabilities, but perhaps the best way to learn more about Perl is to read its *perlfunc* document, which lists all the available Perl functions and their usage. You can view this document by using the `perldoc` script and typing `perldoc perlfunc` at the command line. You can also find this document online at http://www.cpan.org/doc/manual/html/pod/perlfunc.html.

## Perl Variables and Data Structures

Perl is a *weakly typed* language, meaning that it does not require that you declare a data type, such as a type of value (data) to be stored in a particular variable. `C`, for example, makes you declare that a particular variable is an integer, a character, a structure, or whatever the case may be. Perl variables are whatever type they need to be, and can change type when you need them to.

### Perl Variable Types

There are three variable types in Perl: *scalars*, *arrays*, and *hashes*. A different character is used to signify each variable type.

Scalar variables are indicated with the `$` character, as in `$penguin`. Scalars can be numbers or strings, and they can change type from one to the other as needed. If you treat a number like a string, it becomes a string. If you treat a string like a number, it is translated into a number if it makes sense to do so; otherwise, it usually evaluates to `0`. For example, the string "`76trombones`" will evaluate as the number `76` if used in a numerical calculation, but the string "polar bear" will evaluate to `0`.

Perl arrays are indicated with the `@` character, as in `@fish`. An array is a list of values that are referenced by index number, starting with the first element numbered 0, just as in C and awk. Each element in the array is a scalar value. Because scalar values are indicated with the `$` character, a single element in an array is also indicated with a `$` character.

For example, `$fish[2]` refers to the third element in the `@fish` array. This tends to throw some people off, but is similar to arrays in C in which the first array element is 0.

Hashes are indicated with the `%` character, as in `%employee`. A hash is a list of name and value pairs. Individual elements in the hash are referenced by name rather than by index (unlike an array). Again, because the values are scalars, the `$` character is used for individual elements.

For example, `%employee{name}` gives you one value from the hash. Two rather useful functions for dealing with hashes are `keys` and `values`. The `keys` function returns an array containing all the keys of the hash, and `values` returns an array of the values of the hash. Using this approach, the Perl program in Listing 30.2 displays all the values in your environment, much like typing the bash shell's `env` command.

### LISTING 30.2 Displaying the Contents of the env Hash

```perl
#!/usr/bin/perl
foreach $key (keys %ENV) {
    print "$key = $ENV{$key}\n";
}
```

### Special Variables

Perl has a wide variety of special variables, which usually look like punctuation—`$_`, `$!`, and `$]`—and are all extremely useful for shorthand code. `$_` is the default variable, `$!` is the error message returned by the operating system, and `$]` is the Perl version number.

`$_` is perhaps the most useful of these, and you will see that variable used often in this chapter. `$_` is the Perl default variable, which is used when no argument is specified. For example, the following two statements are equivalent:

```
chomp;
chomp($_);
```

The following loops are equivalent:

```perl
for $cow (@cattle) {
    print "$cow says moo.\n";
}
for (@cattle) {
    print "$_ says moo.\n";
}
```

For a complete listing of the special variables, you should see the **perlvar** document that comes with your Perl distribution (such as in the **perlvar** manual page), or you can go online to http://theoryx5.uwinnipeg.ca/CPAN/perl/pod/perlvar.html.

# Operators

Perl supports a number of operators to perform various operations. There are *comparison operators* (used to compare values, as the name implies), *compound operators* (used to combine operations or multiple comparisons), *arithmetic operators* (to perform math), and special *string constants*.

## Comparison Operators

The comparison operators used by Perl are similar to those used by C, awk, and the csh shell, and are used to specify and compare values (including strings). Most frequently, a comparison operator is used within an **if** statement or loop. Perl has comparison operators for numbers and strings. Table 30.1 shows the numeric comparison operators and their behavior.

| Operator | Meaning |
| :--- | :--- |
| `==` | Is equal to |
| `<` | Less than |
| `>` | Greater than |
| `<=` | Less than or equal to |
| `>=` | Greater than or equal to |
| `!=` | Not equal to |
| `<=>` | Range of >= first operand to <= second operand; Returns -1 if less than, 0 if equal, and 1 if greater than |

Table 30.2 shows the string comparison operators and their behaviors.

| Operator | Meaning |
| :--- | :--- |
| `eq` | Is equal to |
| `lt` | Less than |
| `gt` | Greater than |
| `le` | Less than or equal to |
| `ge` | Greater than or equal to |
| `ne` | Not equal to |
| `cmp` | Returns -1 if less than, 0 if equal, and 1 if greater than |
| `=~` | Matched by regular expression |
| `!~` | Not matched by regular expression |

## Compound Operators

Perl uses compound operators, similar to those used by C or awk, which can be used to combine other operations (such as comparisons or arithmetic) into more complex forms of logic. Table 30.3 shows the compound pattern operators and their behavior.

**TABLE 30.3 Compound Pattern Operators in Perl**

| Operator | Meaning |
| :--- | :--- |
| `&&` | Logical AND |
| `\|\|` | Logical OR |
| `!` | Logical NOT |
| `()` | Parentheses; used to group compound statements |

## Arithmetic Operators

Perl supports a wide variety of math operations. Table 30.4 summarizes these operators.

**TABLE 30.4 Perl Arithmetic Operators**

| Operator | Purpose |
| :--- | :--- |
| `x**y` | Raises x to the y power (same as x^y) |
| `x%y` | Calculates the remainder of x/y |
| `x+y` | Adds x to y |
| `x-y` | Subtracts y from x |
| `x*y` | Multiplies x times y |
| `x/y` | Divides x by y |
| `-y` | Negates y (switches the sign of y); also known as the *unary minus* |
| `++y` | Increments y by 1 and uses value (prefix increment) |
| `y++` | Uses value of y and then increments by 1 (postfix increment) |
| `--y` | Decrements y by 1 and uses value (prefix decrement) |
| `y--` | Uses value of y and then decrements by 1 (postfix decrement) |
| `x=y` | Assigns value of y to x. Perl also supports operator-assignment operators (`+=`, `-=`, `*=`, `/=`, `%=` , and `**=` and others) |

You can also use comparison operators (such as `==` or `<`) and compound pattern operators (`&&`, `||`, and `!`) in arithmetic statements. They evaluate to the value `0` for false and `1` for true.

## Other Operators

Perl supports a number of operators that don't fit any of the prior categories. Table 30.5 summarizes these operators.

**TABLE 30.5 Other Perl Operators**

| Operator | Purpose |
| :--- | :--- |
| `~x` | Bitwise not (changes 0 bits to 1 and 1 bits to 0) |
| `x & y` | Bitwise and |
| `x \| y` | Bitwise or |
| `x ^ y` | Bitwise exclusive or (XOR) |
| `x << y` | Bitwise shift left (shifts x by y bits) |
| `x >> y` | Bitwise shift right (shifts x by y bits) |
| `x . y` | Concatenate y onto x |
| `a x b` | Repeats string a for b number of times |
| `x , y` | Comma operator—evaluates x and then y |
| `x ? y : z` | Conditional expression—if x is true, y is evaluated; otherwise, z is evaluated |

Except for the comma operator and conditional expression, these operators can also be used with the assignment operator similar to the way addition (+) can be combined with assignment [+=], giving -=.

## Special String Constants

Perl supports string constants that have special meaning or cannot be entered from the keyboard. Table 30.6 shows most of the constants supported by Perl.

**TABLE 30.6 Perl Special String Constants**

| Expression | Meaning |
| :--- | :--- |
| `\\` | The means of including a backslash |
| `\a` | The alert or bell character |
| `\b` | Backspace |
| `\cC` | Control character (like holding the Ctrl key down and pressing the C character) |
| `\e` | Escape |
| `\f` | Formfeed |
| `\n` | Newline |
| `\r` | Carriage return |
| `\t` | Tab |
| `\xNN` | Indicates that NN is a hexadecimal number |
| `\oNNN` | Indicates that NNN is an octal (base 8) number |

## Conditional Statements: if/else and unless

Perl offers two conditional statements, *if* and *unless*, which function opposite one another. *if* enables you to execute a block of code only if certain conditions are met so that you can control the flow of logic through your program. Conversely, *unless* performs the statements when certain conditions are not met. The following sections explain and demonstrate how to use these conditional statements when writing scripts for Linux.
