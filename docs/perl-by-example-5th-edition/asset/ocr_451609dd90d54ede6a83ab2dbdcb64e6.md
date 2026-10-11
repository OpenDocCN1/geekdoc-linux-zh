and $b, not the normal @_array. (See Chapter 11, "How Do Subroutines Function?" for further discussion.) Do not try to modify $a or $b, as they represent the values that are being sorted. If you want Perl to sort your data according to a particular locale, your program should include the use locale pragma. For a complete discussion, see perldoc perl perllocale.

# FORMAT

```
sort(SUBROUTINE LIST)
sort(LIST)
sort SUBROUTINE LIST
sort LIST
```

# EXAMPLE 3.39

(The Script)

```
use warnings;
# Simple alphabetic sort
1 my @list = ("dog", "cat", "bird", "snake");
  print "Original list: @list\n";
2 my @sorted = sort @list;
  print "ASCII sort: @sorted\n";

# Reversed alphabetic sort
4 @sorted = reverse sort @list;
  print "Reversed ASCII sort: @sorted\n";
```

(Output)

```
Original list: dog cat bird snake
ASCII sort: bird cat dog snake
Reversed ASCII sort: snake dog cat bird
```

# EXPLANATION

+   1  The @list array will contain a list of items to be sorted.
+   2  The sort function performs a string (lexicographical for current locale) sort on the items. The sorted values must be assigned to another list or the same list. The sort function doesn't change the original list.
+   3  The sorted string is printed.
+   4  This list is sorted alphabetically and then reversed.

# ASCII and Numeric Sort Using Subroutine

You can either define a subroutine or use an inline function to perform customized sorting, as shown in the following examples. A note about $a and $b: they are special global Perl variables used by the sort function for comparing values. If you need more information on the operators used, see Chapter 6, "Where's the Operator?"