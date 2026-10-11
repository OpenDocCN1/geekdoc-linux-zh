354

Chapter 11   •   How Do Subroutines Function?

# EXPLANATION

+   1  Scalars are assigned values.
+   2  The greeting subroutine is called with two parameters, $first and $last.
+   3  The subroutine is declared.
+   4  The parameters are stored in the @_ array, a local array that is created when the subroutine is entered and is removed when the subroutine exits. It contains references to the $first and $last.
+   5  The first two elements of the @_ array are printed. The individual elements are represented as scalars $_[0] and $_[1].
+   6  The closing curly brace marks the end of the subroutine definition. @_ will disappear.

# EXAMPLE 11.5

```
(The Script)
# Subroutine to add a list of numbers
use warnings;
1  my @m = (1...100);   # Create an array of 100 numbers
   my @n = (2...29);

2  addemp(@m, @n);     # Pass two arrays
   addemp(1,3,5,7);    # Pass a list

4  sub addemp{
5    print "@_\n";     # print values in @_
6    my $sum=0;         # Initialize $sum
7    foreach my $n (@_) {
      $sum += $n;
    }
*    print "The sum is $sum.\n";
      print "=" x 30, "\n";
   }
```

```
(Output)
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28
29 30 31 32 33 34 35 36 37 38 39 40 41 42 43 44 45 46 47 48 49 50 51 52 53
54 55 56 57 58 59 60 61 62 63 64 65 66 67 68 69 70 71 72 73 74 75 76 77 78
79 80 81 82 83 84 85 86 87 88 89 90 91 92 93 94 95 96 97 98 99 100 2 3 4 5
6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29
----------------------------
The sum is 5484.
----------------------------
1 3 5 7
The sum is 16.
```

# EXPLANATION

+   1  Two arrays, @m and @n, are assigned a range of numbers.
+   2  The addemp() subroutine is called with two arrays as arguments (also called actual parameters). The foreach loop assigns, in turn, to scalar $value each element of the @_ array.