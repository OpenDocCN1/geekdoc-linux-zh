# 5.3 Array Functions



# EXAMPLE 5.40

```
(The Script)
use warnings;
my @list=("dog","cat","bird","snake");
print "Original list: @list\n";
# ASCII sort using a subroutine
sub asc_sort{
$@ cmp $b; # Sort ascending order
}
@sorted_list=sort asc_sort(@list);
print "ASCII sort: @sorted_list\n";
# Numeric sort using subroutine
sub numeric_sort{
$@ <=> $b; # $a and $b are compared numerically
}
@number_sort=sort numeric_sort 10, 0, 5, 9.5, 10, 1000;
print "Numeric sort: @number_sort\n";
```

(Output)
Original list: dog cat bird snake
ASCII sort: bird cat dog snake
Numeric sort: 0 5 9.5 10 10 1000.

# EXPLANATION

+   1. The @list array will contain a list of items to be sorted.
+   2. The subroutine asc_sort() is sent a list of strings to be sorted.
+   3. The special global variables $a and $b are used when comparing the items to be sorted in ascending order. If $a and $b are reversed (for example, $b cmp $a), then the sort is done in descending order. The cmp operator is used when comparing strings.
+   4. The sort function sends a list to the asc_sort(), user-defined subroutine, where the sorting is done. The sorted list will be returned and stored in @sorted_list.
+   5. This is a user-defined subroutine, called numeric_sort(). The special variables $a and $b compare the items to be sorted numerically, in ascending order. If $a and $b are reversed (for example, $b <=> $a), then the sort is done in numeric descending order. The <=> operator is used when comparing numbers.
+   6. The sort function sends a list of numbers to the numeric_sort() function and gets back a list of sorted numbers, stored in the @number_sort array.