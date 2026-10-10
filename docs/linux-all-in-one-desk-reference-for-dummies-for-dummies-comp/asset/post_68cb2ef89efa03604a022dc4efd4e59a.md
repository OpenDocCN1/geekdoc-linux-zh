
## Scalars

A *scalar variable* can store a single value, such as a number or a text string. Scalar variables are the basic data type in Perl. Each scalar's name begins with a dollar sign ($). Typically, you start using a scalar with an assignment statement that initializes it. You can even use a variable without initializing it; the default value for numbers is zero, and the default value of a string is an empty string. If you want to see whether a scalar is defined, use the defined function as follows:

```perl
print "Name undefined!\n" if !(defined $name);
```

The expression (defined $name) is 1 if $name is defined. You can *undefine* a variable by using the undef function. You can undefine $name, for example, as follows:

```perl
undef $name;
```

Variables are evaluated according to context. Following is a script that initializes and prints a few variables:

```perl
#!/usr/bin/perl
$Title = "Linux All-in-One Desk Reference For Dummies";
$count1 = 650;
$count2 = 166;
$total = $count1 + $count2;
print "Title: $Title -- $total pages\n";
```

When you run the preceding Perl program, it produces the following output:

```
Title: Linux All-in-One Desk Reference For Dummies -- 816 pages
```

As the Perl statements show, when the two numeric variables are added, their numeric values are used; but when the $total variable prints, its string representation displays.

Another interesting aspect of Perl is that it evaluates all variables in a string within double quotation marks (" . . . "). However, if you write a string inside single quotation marks (' . . . '), Perl leaves that string untouched. If you write

```perl
print 'Title: $Title -- $total pages\n';
```

with single quotes instead of double quotes, Perl displays

```
Title: $Title -- $total pages\n
```

and does not generate a new line.

![](img/11709a8f88c8cd03868a929dc94c0e2b_774_0.png)

A useful Perl variable is $_ (the dollar sign followed by the underscore character). This special variable is known as the default argument. The Perl interpreter determines the value of $_ depending on the context. When the Perl interpreter reads input from the standard input, $_ holds the current input line; when the interpreter is searching for a specific pattern of text, $_ holds the default search string.

## Arrays

In Perl, an array is a collection of scalars. The array name begins with an at symbol (@). As in C, array subscripts start at zero. You can access the elements of an array with an index. Perl allocates space for arrays dynamically.

Consider the following simple script:

```perl
#!/usr/bin/perl
@commands = ("start", "stop", "draw", "exit");
$ncmpd = @commands;
print "There are $ncmpd commands.\n";
print "The first command is: $commands[0]\n";
```

When you run the script, it produces the following output:

```
There are 4 commands.
The first command is: start
```

As you can see, equating a scalar to the array sets the scalar to the number of elements in the array. The first element of the @commands array is referenced as $commands[0] because the index starts at zero. Thus, the fourth element in the @commands array is $commands[3].

Two special scalars are related to an array. The $[ variable is one of them, and it's current base index (the starting index), which is zero by default. The other scalar is $arrayname (in which arrayname is the name of an array variable), which has the last array index as the value. Thus, for the @commands array, $commands is 3.

You can print an entire array with a simple print statement like this:

```perl
print "@commands\n";
```

When Perl executes this statement, it displays the following output:

```
start stop draw exit
```

## Associative arrays

*Associative array* variables, which are declared with a percent sign (%) prefix, are unique features of Perl. Using associative arrays, you can index an array with a string, such as a name. A good example of an associative array is the %ENV array that Perl automatically defines for you. In Perl, %ENV is the array of environment variables that you can access by using the environment variable name as an index. The following Perl statement prints the current PATH environment variable:

```perl
print "PATH = $ENV{PATH}\n";
```

When Perl executes this statement, it prints the current setting of PATH. In contrast to indexing regular arrays, you have to use braces to index an associative array.

Perl has many built-in functions — such as *delete, each, keys, and values* — that enable you to access and manipulate associative arrays.

## Predefined variables in Perl

Perl has several predefined variables that contain useful information you may need in a Perl script. Following are a few important predefined variables:

- **@ARGV** is an array of strings that contains the command-line options to the script. The first option is $ARGV[0], the second one is $ARGV[1], and so on.
- **%ENV** is an associative array that contains the environment variables. You can access this array by using the environment variable name as a key. To access each element in the array, change the percent sign to a dollar sign and enclose the key in parentheses. For example, $ENV{HOME} is the home directory, and $ENV{PATH} is the current search path that the shell uses to locate commands.
- **$_** is the default argument for many functions. If you see a Perl function used without any argument, the function probably is expecting its argument to be contained in the $_ variable.
- **@_** is the list of arguments passed to a subroutine.
- **$0** is the name of the file containing the Perl program.
- **$]** is the version number of Perl you are using (for example, if you use Perl Version 5.8.7, $] will be 5.008007).
- **$<** is the user ID (an identifying number) of the user running the script.
- **$$** is the script’s process ID.
- **$?** is the status the last system call has returned.

## Operators and expressions

Operators are used to combine and compare Perl variables. Typical mathematical operators are addition (+), subtraction (-), multiplication (*), and division (/). Perl and C provide nearly the same set of operators. When you use operators to combine variables, you end up with expressions. Each expression has a value.

Here are some typical Perl expressions:

```perl
error < 0
$count == 10
$count + $i
$users{$1}
```

These expressions are examples of the comparison operator (the first two lines), the arithmetic operator, and the array-index operator.

> In Perl, don’t use the == operator to determine whether two strings match; The == operator works only with numbers. To test the equality of strings, Perl includes the FORTRAN-style eq operator. Use eq to see whether two strings are identical, as follows:

```perl
if ($input eq "stop") { exit; }
```

Other FORTRAN-style, string-comparison operators include ne (inequality), lt (less than), gt (greater than), le (less than or equal to), and ge (greater than or equal to). Also, you can use the cmp operator to compare two strings. The return value is -1, 0, or 1, depending on whether the first string is less than, equal to, or greater than the second string.

Perl also provides the following unique operators. C lacks an exponentiation operator, which FORTRAN includes; Perl uses ** as the exponentiation operator. Thus, you can write the following code in Perl:

```perl
$x = 2;
$y = 3;
$z = $x ** $y; # z should be 8 (2 raised to the power 3)
$y **= 2; # y is now 9 (3 raised to the power 2)
```

You can initialize an array to null by using () — the null-list operator — as follows:

```perl
@commands = ();
```

The dot operator (.) enables you to concatenate two strings, as follows:

```perl
$part1 = "Hello, ";
$part2 = "World!";
```

```perl
$message = $part1 . $part2; # Now $message = "Hello, World!"
```

The repetition operator, denoted by `x`, is interesting and quite useful. You can use the `x` operator to repeat a string a specified number of times. Suppose that you want to initialize a string to 65 asterisks (`*`). The following example shows how you can initialize the string with the `x` operator:

```perl
$marker = "*";
$marker x= 65; # Now $marker is a string of 65 asterisks
```

Another powerful operator in Perl is `range`, which is represented by two periods (`..`). You can initialize an array easily by using the range operator. Following are some examples:

```perl
@numerals = (0..9); # @numerals = 0, 1, 2, 3, 4, 5, 6, 7, 8, 9
@alphabet = ('A'..'Z'); # @alphabet = capital letters A through Z
```

## Regular expressions

If you have used any UNIX or Linux system for a while, you probably know about the `grep` command, which enables you to search files for a pattern of strings. Following is a typical use of `grep`:

```bash
cd /usr/include
grep "[Ll]inux" *.h | more
```

The preceding `grep` command finds all occurrences of **Linux** or **linux** in the files with names ending in `.h`.

The `grep` command's "[Ll]inux" argument is known as a regular expression, a pattern that matches a set of strings. You construct a regular expression with a small set of operators and rules that resemble the ones for writing arithmetic expressions. A list of characters inside brackets ([ ]), for example, matches any single character in the list. Thus, the regular expression "[Ll]inux" is a set of two strings, as follows:

```
Linux
linux
```

Perl supports regular expressions, just as the `grep` command does. Many other Linux programs, such as the `vi` editor and `sed` (the stream editor), also support regular expressions. The purpose of a regular expression is to search for a pattern of strings in a file. That's why editors support regular expressions.

You can construct and use complex regular expressions in Perl. The rules for these regular expressions are fairly simple. Essentially, the regular expression is a sequence of characters in which some characters have special meaning. Table 4-1 summarizes the basic rules for interpreting the characters used to construct a regular expression.
