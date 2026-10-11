# A Reference to a List of Lists

In the following example, a reference points to an anonymous list of lists. Notice that in this example, `$matrix` is a reference to an anonymous array in square brackets, whereas in the previous example, `@matrix` is a named array with parentheses to contain its values. This distinction is important as it is a common error to use `/` when one should use `()`, and vice versa.

# EXAMPLE 12.7

```
(The Script)
  use warnings;
  use strict;
  # A reference to a two-dimensional array
1  my $matrix = [
       [ 0, 2, 4 ],
       [ 4, 1, 32 ],
       [ 12, 15, 17 ]
     ];
2  print "Row 3 column 2 is $matrix->[2]->[1].\n";
3  print "Dereferencing with two loops.\n";
4  for(my $x=0; $x<3; $x++){ 
5    for(my $y=0;$y<3;$y++){ 
6      print "$matrix->[$x]->[$y] ";
     }
   }
  print "\n";
7  print "Dereferencing with one loop.\n";
8  for(my $i=0; $i < 3; $i++){
9    print "@{$matrix->[$i]}\n";
  }

(Output)
2  Row 3 column 2 is 15.
3  Dereferencing with two loops.
   0  2  4
   4  1  32
   12 15 17
7  Dereferencing with one loop.
   0 2 4
   4 1 32
   12 15 17
```