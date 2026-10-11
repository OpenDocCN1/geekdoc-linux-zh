# EXAMPLE 5.5 (CONTINUED)

```
(Output)
6  5
7  John Smith
8  I need $125.75.
9  John Smith gave me $125.75.
10 The time is Sat Jan 24 16:12:49 2014.
11 The month is January.
12 The month is January.
```

# EXPLANATION

1 The scalar $num is assigned the numeric literal, 5.
2 The scalar $friend is assigned the string literal, John Smith.
3 The scalar $money is assigned the numeric floating point literal, 125.75.
5 The scalar $now is assigned the output of Perl's built-in localtime function.
5 The scalar $month is assigned jan.
8 The quoted string is printed. The backslash allows the first dollar sign ($) to be printed literally; the value of $money is interpolated within double quotes, and its value printed.
9 The Perl qq construct replaces double quotes. The string to be quoted is enclosed in forward slashes. The value of the scalar $friend is interpolated; a literal dollar sign precedes the value of the scalar interpolated variable, $money.
10 The quoted string is printed as it in double quotes. The $now variable is interpolated.
11 Curly braces can be used to shield the variable from characters that are appended to it January will be printed.
12 Normally, two strings or expressions are joined together with the dot operator (see Chapter 6, "Where's the Operator?"), called the concatenation operator.

**The defined Function.** If a scalar has neither a valid string nor a valid numeric value, it is *undef*. The *defined* function allows you to check for the validity of a variable's value. It returns 1 if the variable has a value (other than *undef*) and nothing if it does not.

# EXAMPLE 5.6

```
$name="Tommy";
print "OK \n" if defined $name;
```

**The undef Function.** When you define a variable without giving it a value, such as my $name; the initial value is *undef*.