
## EXAMPLE 12.12

```perl
(The Script)
1  my $subref = sub { print @_ };
2  $subref->('a', 'b', 'c');
   print "\n";

(Output)
1  abc
```

## EXPLANATION

- 1. The scalar `$subref` is assigned a reference to an anonymous subroutine. The only function of the subroutine is to print its arguments stored in the `@_` array.
- 2. The subroutine is called via its reference and passed three arguments.

**Subroutines and Passing by Reference.** When passing arguments to subroutines, they are sent to the subroutine and stored in the `@_` array. If you have a number of arguments—say an array, a scalar, and another array—the arguments are all flattened out onto the `@_` array. It would be hard to tell where one argument ended and the other began unless you also passed along the size of each of the arrays, and then the size would be pushed onto the `@_` array and you would have to get that to determine where the first array ended, and so on. The `@_` could also be quite large if you are passing a 1,000-element array. So, the easiest and most efficient way to pass arguments is by reference, as shown in Example 12.13.

## EXAMPLE 12.13

```perl
(The Script)
use strict;
use warnings;
1  my @toys = qw(Buzzlightyear Woody Bo);
2  my $num = @toys;    # Number of elements in @toys is assigned to $num
3  gifts(\$num, \@toys);    # Passing by reference

4  sub gifts {
5  my($n, $t) = @_;    # Copy references to $n and $t
6  print "There are $$n gifts: ";
7  print "@$t\n";
8  push(@{$t}, 'Janey', 'Slinky');
9  }

9  print "The original array was changed to: @toys\n";

(Output)
6,7  There are 3 gifts: Buzzlightyear Woody Bo
9  The original array was changed to: Buzzlightyear Woody Bo Janey Slinky
```

## EXPLANATION

- 1. The array `@toys` is assigned three values.
- 2. The scalar `$num` is assigned the number of elements in the `@toys` array (Remember, a scalar contains only one value, so when you assign an array to a scalar, the number of elements in the array is assigned to the scalar).
- 3. The subroutine `gifts` is called with two references as parameters.
- 4. The subroutine is entered.
- 5. The `@_` array contains the two references. The values of the references are copied into two lexical variables, `$n` and `$t`.
- 6. The reference to the scalar is dereferenced. It points to the scalar `$num`.
- 7. The reference to the array is dereferenced. It references the array `@toys`.
- 8. The `push` function adds two new elements to the array referenced by `$t`.
- 9. After exiting the subroutine, `@toys` is printed with its new values.

## EXAMPLE 12.14

```perl
(The Script)
use strict;
use warnings;
# This script demonstrates the use of references
# to pass arrays. Instead of passing the entire
# array, a reference is passed.
# The value of the last expression is returned.

my $list1 = (1 .. 100);
my $list2 = (5, 10, 15, 20);
print "The total is : ", addemup( \$list1, \$list2), "\n";
#    Two references are passed
sub addemup{
    my( $sarr1, $sarr2 ) = @_;
    # @_ contains two references
    my $total;
    print $sarr1, "\n" ;
    print $sarr2, "\n";

    foreach my $sum ( @{$sarr1}, @{$sarr2} ){
        $total += $sum;
    }

    return $total; # The expression is evaluated and returned
}

(Output):
7 ARRAY(0x8a62d68)
6 ARRAY(0x8a60f2c)
3 The total is: 5100.
```

## EXPLANATION

- 1. The array `@list1` is assigned a list of numbers between 1 and 100.
- 2. The array `@list2` is assigned the list of numbers 5, 10, 15, and 20.
- 3. The `addemup` subroutine is called. Two arguments are passed. The backslash preceding each of the arrays causes references to be passed.
- 4. The subroutine `addemup` is declared and defined.
- 5. The references are passed to the `@_` array and assigned to `my` variables `$sarr1` and `$sarr2`, respectively.
- 6. The `my` variable `$total` is declared.
- 7, 8. The addresses of the references are printed.
- 9. The `foreach` loop is entered. `@$sarr1` and `@$sarr2` dereference the references, creating a list of array elements to be processed, one at a time.
- 10. Each time through the loop, `$total` accumulates the sum of `$total + $sum`.
- 11. The sum is returned to where the subroutine was called on line 3. Since the subroutine was called as an argument to the `print` function, the results will be printed after they are returned from the subroutine.

### 12.1.6 The ref Function

The `ref` function is used to test for the existence of a reference. It returns a non-empty string if its argument is a reference; with no argument, `$_` is used. The string returned is the type of data the reference points to; for example, `SCALAR` is returned if the reference points to a scalar, and `ARRAY` is returned if it points to an array. If the argument is not a reference, the empty string is returned. Table 12.1 lists the values returned by the `ref` function.

**Table 12.1 Return Values \* from the `ref` Function**

| What Is Returned | Meaning |
| :--- | :--- |
| REF | Reference to reference |
| SCALAR | Reference to scalar |
| ARRAY | Reference to array |
| HASH | Reference to hash |
| CODE | Reference to subroutine |
| GLOB | Reference to typeglob |

\* For a complete list, see `perldoc -l ref`.

## EXAMPLE 12.15

```perl
(The Script)
use warnings;
use strict;
1
sub gifts;		# Forward declaration
2
my $num = 5;
3
my $junk = "xxxx";
4
my @toys = qw/Buzzlightyear Woody Thomas/ ;
5
gifts( $num, @toys, $junk );
6
sub gifts {
7
	my ( $n, @t, $j) = @_;
8
	print "$n is a reference.\n" if ref($n);
9
	print "$t is a reference.\n" if ref($t);
10
	print "$j is not a reference.\n" if ref($j);
11
	printf "$n is a reference to a %s.\n", ref($n);

(Output)
8 $n is a reference.
9 $t is a reference.
10 $n is a reference to a SCALAR.
11 $t is a reference to an ARRAY.
```

## EXPLANATION

- 1. The subroutine `gifts` is a forward declaration, allowing Perl to know it is a subroutine defined somewhere in the program. You will not need parentheses to call the subroutine if it is declared before it is defined.
- 2. The scalar `$num` is assigned 5.
- 3. The scalar `$junk` is assigned the string `xxxx`.
- 4. The array `@toys` is assigned a list.
- 5. The subroutine `gifts` is called. The first two variables are passed as references by preceding them with a backslash. The last variable, `$junk`, is not passed as a reference.
- 6. The subroutine `gifts` is defined.
- 7. The values assigned to the `@_` array, in this case, two references (addresses) and one nonreference, will be assigned to `$n`, `$t`, and `$j`, respectively.
- 8. The `ref` function is called with a reference, `$n`, as its argument. The line will be printed only if the variable `$n` is a reference.
- 9. `$j` is not a reference. The return value for the `ref` function is null.
- 10. The `printf` function prints the value of the data type returned from `ref`, a scalar.
- 11. The `printf` function prints the value of the data type returned from `ref`, an array.

## 12.1.7 Symbolic References

A hard reference is a scalar variable that holds the address of another type of data. This chapter focused on hard references. This is an example of the value of a hard reference:

```
ARRAY (0x7f9241004ee8)
```

A symbolic reference names another variable rather than just pointing to a value; that is, it doesn't contain the data type and address. Their use is discouraged because they cannot be lexically scoped, and will not get past `strict` if you have it turned on. You would see something like this: *Global symbol `$animal' requires explicit package name at symbolic reference line 3.*

Example 12.16 demonstrates a `symbolic` reference where the value of one variable references the name of another variable. For more on symbolic references, see http://perlmon.com/symbolic-reference-in-perl.

![](img/8556abcb353c0991f12099420ec28735_427_0.png)

```perl
 # Program using symbolic references
    use feature qw(say);
 1  $animal='dog';
 2  $dog='Lady';
 3  say "Your dog is called ${$animal}";  # Symbolic reference
 4  ${$animal}='Lassie';
 5  say "Why don't you call her ${$animal}?";

  # Now create symbolic references for an array, hash, and subroutine
 6  @letters = ('a'..'z'); # Create an array
 7  %capital = {'Maine'=>'Portland',
               'California'=>'Sacramento',
               'Montana'=>'Helena'};
 8  sub greetme { print "hello\n"}
 9  $refarray = "letters"; # Create symbolic references
10  $refhash = "capital";
11  $refsub = "greetme";

12  say "The array: @{$refarray}"; # Get the values in the array
13  say "The first element in the array: ${$refarray[0]}";
14  say "Call to greetme(): "，  &{$refsub}; # Call to subroutine greetme

(Output)
 3  Your dog is called Lady
 5  Why don't you call her Lassie?
12  The array: a b c d e f g h i j k l m n o p q r s t u v w x y z
13  The first element in the array: a
14  Call to greetme(): hello
```
