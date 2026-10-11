# EXAMPLE 5.41

```
```
# (The Script)
use warnings;
# Sorting numbers with block
1 my @sorted_numbers = sort {$a <=> $b} (3,4,1,2);
2 print "The sorted numbers are: @sorted_numbers", "\n";
# (Output)
2 The sorted numbers are: 1 2 3 4.
```
```

# EXPLANATION

+   1.  The sort function is given a block, also called an **inline subroutine**, to sort a list of numbers passed as arguments. The `<=>` operator is used with variables `$a` and `$b` to compare the numbers. The sorted numeric list is returned and stored in the array `@sorted_numbers`. (See <http://perldoc.perl.org/functions/sort.html> for more on the sort function).
+   2.  The sorted list is printed.

# 5.3.9 Checking the Existence of an Array Index Value

**The exists Function.** The `exists` function returns **true** if an array index (or hash key) has been defined, and **false** if it has not. It is most commonly used when testing a hash key's existence.

# FORMAT

```
`exists $ARRAY[index];`
```

# EXAMPLE 5.42

```
```
use warnings;
1 my @names = qw(Tom Raul Steve Jon);
2 print "Hello $names[1]\n", if exists $names[1];
3 print "Out of range!\n", if not exists $names[5];
# (Output)
2 Hello Raul
3 Out of range!
```
```

# EXPLANATION

+   1.  An array of names is assigned to `@names`.
+   2.  If the index *1* is defined, the `exists` function returns `true` and the string is printed.
+   3.  If the index *5* does not exist (and in this example it doesn't), then the string *Out of range!* is printed.