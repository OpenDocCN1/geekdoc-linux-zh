when necessary, you can use strings and numbers interchangeably. Perl interprets scalar variables as strings when it makes sense to interpret them as strings, and as numbers when it makes sense to interpret them as numbers. Perl’s judgment in these matters is generally good.

The following example shows some uses of scalar variables. The first two lines of code (lines 3 and 4) assign the string Sam to the scalar variable $name and the numbers 5 and 2 to the scalar variables $n1 and $n2, respectively. In this example, multiple statements, each terminated with a semicolon (;), appear on a single line. See use feature ‘say’ on page 981 if this program complains about say not being available.

```
$ cat scalars1.pl
#1/usr/bin/perl -w

$name = "Sam";
$n1 = 5; $n2 = 2;

say "$name $n1 $n2";
say "$name $n1 $n2";
say $n1 + $n2, "", $n1 * $n2;
say $name + $n1;

$ ./scalars1.pl
Sam 5 2
5 + 2
$name $n1 $n2
7 10
Argument "Sam" isn't numeric in addition (+) at ./scalars1.pl line 11.
5
```

Double quotation marks The first say statement sends the string enclosed within double quotation marks to standard output (the screen unless you redirect it). Within double quotation marks, Perl expands variable names to the value of the named variable. Thus the first say statement displays the values of three variables, separated from each other by spaces. The second say statement includes a plus sign (+). Perl does not recognize operators such as + within either type of quotation marks. Thus Perl displays the plus sign between the values of the two variables.

Single quotation marks The third say statement sends the string enclosed within single quotation marks to standard output. Within single quotation marks, Perl interprets all characters literally, so it displays the string exactly as it appears between the single quotation marks.

In the fourth say statement, the operators are not quoted, and Perl performs the addition and multiplication as specified. Without the quoted spaces, Perl would concatenate the two numbers (710). The last say statement attempts to add a string and a number; the -w option causes Perl to display an error message before displaying 5. The 5 results from adding Sam, which Perl evaluates as 0 in a numerical context, to the number 5 (0 + 5 = 5).