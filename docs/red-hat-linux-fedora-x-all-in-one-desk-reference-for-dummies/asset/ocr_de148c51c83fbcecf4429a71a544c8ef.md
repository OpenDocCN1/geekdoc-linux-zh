# 788 Getting an Overview of Perl

![](bbox=[0.14, 0.134, 0.219, 0.209])

In Perl, don't use the == operator to determine whether two strings match; the == operator works only with numbers. To test the equality of strings, Perl includes the FORTRAN-style eq operator. Use eq to see whether two strings are identical, as follows:

```
if ($input eq "stop") { exit; }
```

Other FORTRAN-style, string-comparison operators include ne (inequality), lt (less than), gt (greater than), le (less or equal), and ge (greater or equal). You can use the cmp operator to compare two strings. The return value is -1, 0, or 1, depending on whether the first string is less than, equal to, or greater than the second string.

Perl also provides the following unique operators. C lacks an exponentiation operator; Perl uses ** as the exponentiation operator. Thus, you can write the following code in Perl:

```
$x = 2;
$y = 3;
$z = $x**$y; # z should be 8 (2 raised to the power 3)
$y **=2; # y is now 9 (3 raised to the power 2)
```

You can initialize an array to null using () — the null-list operator — as follows:

```
@commands = ();
```

The dot operator (.) enables you to concatenate two strings, as follows:

```
$part1 = "Hello, ";
$part2 = "World";
$message = $part1.$part2; # Now message = "Hello, World!"
```

The repetition operator, denoted by *, is interesting and quite useful. You can use the x= to repeat a string specified number of times. Suppose you want to initialize a string with 65 asterisks (*). The following example shows how you can initialize the string with the x= operator:

```
$marker = "*\";n$marker x = 65; # Now marker is a string of 65 asterisks"
```

Another powerful feature in Perl is range, is represented by two periods (.. You can initialize an array easily using the range operator. Following are some examples:

```
@numerals = (0..9); @numerals = 0, 1, 2, 3, 4, 5, 6, 7, 8, 9
@alphabet = ('A'..'Z'); @alphabet = capital letters A through Z
```