# ARRAY VARIABLES

An array variable is an ordered container of scalars whose name begin with an sign (@) and whose first element is numbered zero (zero-based indexing). Because an array can hold zero or more scalars, it is a plural variable. Arrays are ordered; hashes (page 1056) are unordered. In Perl, arrays grow as needed. If you reference an uninitialized element of an array, such as an element beyond the end of the array, Perl returns undef.

The first statement in the following program assigns the values of two numbers and a string to the array named @arrayvar. Because Perl uses zero-based indexing, the first say statement displays the value of the second element of the array (the element with index 1). This statement specifies the variable $arrayvar[1] as a scalar (singular) because it returns a single value. The second say statement specifies the variable @arrayvar[1,2] as a list (plural) because it returns multiple values (with the indexes 1 and 2).

```
$ cat array1.pl
!/usr/bin/perl -w
@arrayvar = (8, 18, "Sam")
say $arrayvar[1];
say "@arrayvar[1,2]";
```

```
$ perl array1.pl
18
Sam
```

The next example shows a couple of ways to determine the length of an array and presents more information on using quotation marks within print statements. The first assignment statement in array2.pl assigns values to the first elements of the @arrayvar2 array. When used in a scalar context, Perl evaluates the name of an array as the length of the array. The second assignment statement assigns the number of elements in @arrayvar2 to the scalar variable Snum.

```
$ cat array2.pl
!/usr/bin/perl -w
@arrayvar2 = ("apple", "bird", 44, "Tike", "metal", "pike");
```

```
$num = @arrayvar2;
print "Elements: ", $num, "\n"; # number of elements in array
print "Elements: $num\n"; # two equivalent print statements
```

```
print "Last: \$$arrayvar2\n";      # index of last element in array
$ ./array2.pl
Elements: 6
Elements: 6
Last: 5
```

The first two print statements in array2.pl display the string Elements:, a SPACE, the value of $num, and a NEWLINE, each using a different syntax. The first of these