
## The Backslash Operator.

The backslash unary operator is used to create a reference, similar to the & used in C to get the "address of." In the following example, `$p` is a scalar that is assigned a reference to `$x`.

```perl
$x = "Tom";
$p = \$x;    # $p gets the memory address of $x
```

Examples of hard references from the Perl *man* page *perlref* include the following:

```perl
$scalarref  = \$foo;       # reference to scalar $foo
$arrayref   = \@ARGV;       # reference to array @ARGV
$hashref    = \%ENV;       # reference to hash %ENV
$coderef    = \&handler;   # reference to subroutine handler
$globref    = \*STDOUT;    # reference to typeglob STDOUT
$refref     = \\\@scalarref;  # reference to another reference
                             (pointer to pointer, ugh)
```

## Dereferencing the Pointer.

If you print the value of a reference, you will see a data type and a hexadecimal address.

```perl
@list = qw(Tom Dick Harry);
$ref = \@list;  # $ref contains the data type and memory address of @list
```

![](img/8556abcb353c0991f12099420ec28735_408_0.png)

If you want to go to the address that *$ref* points to (that is, the address of @list), and get the values stored there, you would say:

```perl
print @{$ref};    # prints Tom Dick and Harry
```

This is called **dereferencing the pointer**. Notice the $ref (the address) is prepended with the @ sign. That tells Perl to get the array values from @list. (Although the curly braces aren't necessary in this example, they will be later on in more complex examples.) The first is the dollar sign, because the reference itself is a scalar. $ref, and then preceding that goes the sigil, representing the type of data it references. In the following examples, we will get into much more detail about how to use references.

## EXAMPLE 12.1

```perl
use warnings;
my $num=5;
my $p = \$num; # $p is assigned the address of $num
print 'The address assigned $p is ', $p, "\n";
print "The value stored at that address is ${$p}\n"; # dereference
```

**Output**

```
The address assigned $p is SCALAR(0xb057c)
The value stored at that address is 5
```

## EXPLANATION

- 1. The scalar $num is assigned the value 5.
- 2. The scalar $p is a reference and assigned the address of $num. This is the function of the backslash operator.
- 3. The value in $p is printed. Along with an address, Perl also tells you the data type is SCALAR.
- 4. To dereference $p, another dollar sign is prepended to $p. This dollar sign tells Perl that you are looking for the value of the scalar $p references; that is, $num. The curly braces are optional, but a good practice because later, with more complex references, they will be necessary when retrieving or setting values with references.

![](img/8556abcb353c0991f12099420ec28735_409_0.png)

## EXAMPLE 12.2

```perl
use warnings;
use strict;
my @toys = qw( Barbie Elmo Thomas Barney );
my %toy = @toys;
my %games = ('Wintendo' => "Wii", 'Sony' => "PlayStation 4", 'Microsoft' => "XBox One", );
```

## 2.1 What Is a Reference?

### EXAMPLE 12.2 (CONTINUED)

```perl
4 my $ref1 = \$num;  # Create references
5 my $ref2 = \@toys;
6 my $ref3 = \%games;

7 print "There are ${$ref1} toys.\n";   # dereference $ref1
8 print "They are: ", join(", ", @{$ref2}), ".\n";
9 print "Jessica's favorite toy is ${$ref2->[0]}.\n";
10 print "Willie's favorite toy is ${$ref2->[2]}.\n";
11 while ((my $key, my $value) = each(%$ref3))
    {
        print "$key=>$value\n";
    }
12 print "They waited in line for a ${$ref3->{Nintendo}}\n";
```

**Output**

```
There are 4 toys.
They are: Barbie, Elmo, Thomas, Barney.
Jessica's favorite toy is Barbie.
Willie's favorite toy is Thomas.
Microsoft => Xbox One
Sony => PlayStation 4
Nintendo => Wii
They waited in line for a Wii
```

### EXPLANATION

- 1. A list is assigned to the array `@toys`.
- 2. The array `@toys` is assigned to the scalar variable `$num`, returning the number of elements in the array.
- 3. The hash `%games` is assigned key/value pairs.
- 4. `$ref1` is a reference. It is assigned the address of the scalar `$num` by using the backslash operator.
- 5. `$ref2` is also a reference. It contains the address of the array `@toys`.
- 6. The reference `$ref3` is assigned the address of the hash `%games`.
- 7. The reference is dereferenced, meaning: Go to the address that `$ref1` is pointing to and print the value of the scalar stored there.
- 8. The reference is again dereferenced, meaning: Go to the address that `$ref2` is pointing to, get the array, and print it.
- 9. The `->` arrow operator is used to dereference `$ref2` and get the first element of the array. (You could also write this as `${$ref2}[0]`.)
- 10. Again, the `->` arrow operator is used to dereference the pointer and retrieve the third element of the array.
- 11. The `each` function is used to retrieve the keys and values from the hash via its reference. To dereference a hash, the `%` sign precedes the reference variable.
- 12. The `->` arrow operator is used to dereference `$ref3` and get the value of the hash where the key is `Nintendo`. (You could also write this as `${$ref3}{"Nintendo"}.)

## 12.1.2 References and Anonymous Variables

It is not necessary to name a variable to create a reference to it. If an array, hash, or subroutine has no name, it is called **anonymous**. If, for example, an array has no name and its data is assigned to a reference variable, you can use the reference to assign and fetch data from the anonymous array.

Use the **arrow operator** (->, called an **infix operator**, to dereference a reference to anonymous arrays, hashes, and subroutines. Although not really necessary, the arrow operator makes the program easier to read.

### Anonymous Arrays.

Enclose anonymous array elements in square brackets ([ ]). These square brackets are not to be confused with the square brackets used to subscript an array. They represent the address of an unnamed array. The brackets will not be interpolated if enclosed within quotes. Use the arrow (infix) operator to get the individual elements of the array.

## EXAMPLE 12.3

```perl
use warnings;
use strict;
my $arrayref = ['Woody', 'Buzz', 'Bo', 'Mr. Potato Head'];
print "The value of the reference, $arrayref is ",
      $arrayref, "\n";
      # All of these examples dereference $arrayref
print "arrayref->[3]", "\n"; # Preferred method for dereferencing
print "${arrayref}[3]", "\n"; # Dereferencing in alternate way
print "${arrayref}[3]", "\n";
print "@{$arrayref}", "\n";
```

**Output**

```
2  The value of the reference, $arrayref is ARRAY(0x8a6f134)
3  Mr. Potato Head
4  Mr. Potato Head
5  Mr. Potato Head
6  Woody Buzz Bo Mr. Potato Head
```

## EXPLANATION

- 1. The anonymous array is assigned to the array reference `$arrayref`.
- 2. The array reference contains the data type and the hexadecimal address of the anonymous array.
- 3. The fourth element of the array is printed. The reference, `$arrayref`, is followed by the arrow operator pointing to the index value that will be retrieved. This is the preferred method for dereferencing.
- 4. The arrow operator is not needed here. Instead, the two methods in lines 4 and 5 can also access the element.
- 5. The entire array is printed after dereferencing the pointer. Curly braces are required in more complicated structures. It’s a good idea to get used to them now.

### Anonymous Hashes.

An **anonymous hash** is a hash without a name. Create a reference to it by using curly braces ({}). You can mix array and hash composers to produce complex data types. These braces are not the same braces that are used when subscripting a hash. The anonymous hash is assigned to a scalar reference.

## EXAMPLE 12.4

![](img/8556abcb353c0991f12099420ec28735_412_0.png)

## EXPLANATION

![](img/8556abcb353c0991f12099420ec28735_412_1.png)

## 12.1.3 Nested Data Structures

The ability to create references to anonymous data structures lends itself to more complex types. For example, you can have hashes nested in hashes, or arrays of hashes, or arrays of arrays, and so forth.

Just as with simpler references, you dereference the anonymous data structures by prepending the reference with the correct funny symbol (@sigil) that represents its data type. For example, if $p is a pointer to a scalar, you can write $$p to dereference the scalar reference, and if $p is a pointer to an array, you can write @{$p} to dereference the array reference or $$p[0] to get the first element of the array. You can also dereference a reference by treating it as a block. You could write $$p[0] as ${$p}[0] or @{$p}[0]. Sometimes, you use the braces to prevent ambiguity, and sometimes they are necessary so that the funny character dereferences the correct part of the structure.
