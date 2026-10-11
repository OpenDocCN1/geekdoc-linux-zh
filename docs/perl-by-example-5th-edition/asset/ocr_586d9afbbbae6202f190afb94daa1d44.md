# 12.1.2  References and Anonymous Variables

It is not necessary to name a variable to create a reference to it. If an array, hash, or subroutine has no name, it is called **anonymous**. If, for example, an array has no name and its data is assigned to a reference variable, you can use the reference to assign and fetch data from the anonymous array.

Use the **arrow operator** (->, called an **infix operator**, to dereference a reference to anonymous arrays, hashes, and subroutines. Although not really necessary, the arrow operator makes the program easier to read.

# Anonymous Arrays.

Enclose anonymous array elements in square brackets ([ ]). These square brackets are not to be confused with the square brackets used to subscript an array. They represent the address of an unnamed array. The brackets will not be interpolated if enclosed within quotes. Use the arrow (infix) operator to get the individual elements of the array.

# EXAMPLE 12.3

```
(The Script)
```
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
(Output):
```
2  The value of the reference, $arrayref is ARRAY(0x8a6f134)
3  Mr. Potato Head
4  Mr. Potato Head
5  Mr. Potato Head
6  Woody Buzz Bo Mr. Potato Head
```
```

# EXPLANATION

+   1. The anonymous array is assigned to the array reference `$arrayref`.
+   2. The array reference contains the data type and the hexadecimal address of the anonymous array.
+   3. The fourth element of the array is printed. The reference, `$arrayref`, is followed by the arrow operator pointing to the index value that will be retrieved. This is the preferred method for dereferencing.
+   4. The arrow operator is not needed here. Instead, the two methods in lines 4 and 5 can also access the element.
+   6. The entire array is printed after dereferencing the pointer. Curly braces are required in more complicated structures. It’s a good idea to get used to them now.