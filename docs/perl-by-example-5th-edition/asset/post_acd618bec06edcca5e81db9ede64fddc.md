
and $b, not the normal @array. (See Chapter 11, "How Do Subroutines Function?" for further discussion.) Do not try to modify $a or $b, as they represent the values that are being sorted. If you want Perl to sort your data according to a particular locale, your program should include the `use locale` pragma. For a complete discussion, see `perldoc perl perllocale`.

## FORMAT

```
sort(SUBROUTINE LIST)
sort(LIST)
sort SUBROUTINE LIST
sort LIST
```

## EXAMPLE 3.39

(The Script)

```perl
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

## EXPLANATION

-   1. The @list array will contain a list of items to be sorted.
-   2. The sort function performs a string (lexicographical for current locale) sort on the items. The sorted values must be assigned to another list or the same list. The sort function doesn't change the original list.
-   3. The sorted string is printed.
-   4. This list is sorted alphabetically and then reversed.

## ASCII and Numeric Sort Using Subroutine

You can either define a subroutine or use an inline function to perform customized sorting, as shown in the following examples. A note about $a and $b: they are special global Perl variables used by the sort function for comparing values. If you need more information on the operators used, see Chapter 6, "Where's the Operator?".

## 5.3 Array Functions

### EXAMPLE 5.40

(The Script)

```perl
use warnings;
my @list=("dog","cat","bird","snake");
print "Original list: @list\n";
# ASCII sort using a subroutine
sub asc_sort{
    $a cmp $b; # Sort ascending order
}
@sorted_list=sort asc_sort(@list);
print "ASCII sort: @sorted_list\n";
# Numeric sort using subroutine
sub numeric_sort{
    $a <=> $b; # $a and $b are compared numerically
}
@number_sort=sort numeric_sort 10, 0, 5, 9.5, 10, 1000;
print "Numeric sort: @number_sort\n";
```

(Output)

```
Original list: dog cat bird snake
ASCII sort: bird cat dog snake
Numeric sort: 0 5 9.5 10 10 1000.
```

### EXPLANATION

-   1. The @list array will contain a list of items to be sorted.
-   2. The subroutine `asc_sort()` is sent a list of strings to be sorted.
-   3. The special global variables `$a` and `$b` are used when comparing the items to be sorted in ascending order. If `$a` and `$b` are reversed (for example, `$b cmp $a`), then the sort is done in descending order. The `cmp` operator is used when comparing strings.
-   4. The `sort` function sends a list to the `asc_sort()`, user-defined subroutine, where the sorting is done. The sorted list will be returned and stored in `@sorted_list`.
-   5. This is a user-defined subroutine, called `numeric_sort()`. The special variables `$a` and `$b` compare the items to be sorted numerically, in ascending order. If `$a` and `$b` are reversed (for example, `$b <=> $a`), then the sort is done in numeric descending order. The `<=>` operator is used when comparing numbers.
-   6. The `sort` function sends a list of numbers to the `numeric_sort()` function and gets back a list of sorted numbers, stored in the `@number_sort` array.

### EXAMPLE 5.41

(The Script)

```perl
use warnings;
# Sorting numbers with block
1 my @sorted_numbers = sort {$a <=> $b} (3,4,1,2);
2 print "The sorted numbers are: @sorted_numbers", "\n";
```

(Output)

```
2 The sorted numbers are: 1 2 3 4.
```

### EXPLANATION

-   1. The `sort` function is given a block, also called an **inline subroutine**, to sort a list of numbers passed as arguments. The `<=>` operator is used with variables `$a` and `$b` to compare the numbers. The sorted numeric list is returned and stored in the array `@sorted_numbers`. (See <http://perldoc.perl.org/functions/sort.html> for more on the `sort` function).
-   2. The sorted list is printed.

## 5.3.9 Checking the Existence of an Array Index Value

**The `exists` Function.** The `exists` function returns **true** if an array index (or hash key) has been defined, and **false** if it has not. It is most commonly used when testing a hash key's existence.

## FORMAT

```
exists $ARRAY[index];
```

## EXAMPLE 5.42

(The Script)

```perl
use warnings;
1 my @names = qw(Tom Raul Steve Jon);
2 print "Hello $names[1]\n", if exists $names[1];
3 print "Out of range!\n", if not exists $names[5];
```

(Output)

```
2 Hello Raul
3 Out of range!
```

## EXPLANATION

-   1. An array of names is assigned to `@names`.
-   2. If the index *1* is defined, the `exists` function returns `true` and the string is printed.
-   3. If the index *5* does not exist (and in this example it doesn't), then the string *Out of range!* is printed.

## 5.3.10 Reversing an Array

The `reverse` function. The `reverse` function reverses the elements in a list, so that if the values appeared in descending order, now they are in ascending order, or vice versa. In scalar context, it concatenates the list elements and returns a string with all the characters reversed; for example, in scalar context `Hello, there!` reverses to `,erreh! olleH`.

## FORMAT

```
reverse (LIST)
reverse LIST
```

## EXAMPLE 5.43

(In Script)

```perl
use warnings;
my (@names, @reversed);
# Reversing the elements of an array
1 @names=('Bob', 'Dan', 'Tom', 'Guy');
2 print @names "\n";
3 my @reversed=reverse @names, "\n";
4 print "@reversed\n";
```

(Output)

```
2 Bob Dan Tom Guy
4 Guy Tom Dan Bob
```

### EXPLANATION

-   1. The array `@names` is assigned list values.
-   2. The original array is printed.
-   3. The `reverse` function reverses the elements in the list and returns the reversed list. It does not change the original array; that is, the array `@names` is not changed. The reversed items are stored in `@reversed`.
-   4. The reversed array is printed.

## 5.4 Hash (Associative Array) Functions

### 5.4.1 The `keys` function

The `keys` function returns, in random order, an array whose elements are the keys of a hash (see also Section 5.4.2, “The `values` function,” and Section 5.4.3, “The `each` function”). Starting with Perl 5.12, `keys` also returns the index values of an array. In scalar context, it returns the number of keys (or indices).

### FORMAT

```
keys (ASSOC_ARRAY)
keys ASSOC_ARRAY
```

### EXAMPLE 5.44

(In Script)

```perl
use warnings;
my(%weekday, @daynumber, $key);
# The keys function returns the keys of a hash
1 my %weekday= (
    '1'=>'Monday',
    '2'=>'Tuesday',
    '3'=>'Wednesday',
    '4'=>'Thursday',
    '5'=>'Friday',
    '6'=>'Saturday',
    '7'=>'Sunday',
);
2 my @daynumber = keys(%weekday);
3 print "@daynumber\n";
4 foreach $key ( keys(%weekday) ){print "$key ";}
print "\n";
5 foreach $key ( sort keys(%weekday) ){print "$key ";}
print "\n";
```

(Output)

```
6 4 1 3 7 2 5
6 4 1 3 7 2 5
1 2 3 4 5 6 7
```

### EXPLANATION

-   1. The hash `%weekday` is assigned keys and values.
-   2. The `keys` function returns a list of all the keys in a hash. In this example, `@daynumber` is an unordered list of all the keys in the `%weekday` hash.
-   4. The `keys` function returns a list of keys. The `foreach` loop will traverse the list of keys, one at a time, printing the keys.
-   5. The `keys` function returns a list of keys in `%weekday` hash. The list will then be sorted, and finally the `foreach` loop will traverse the sorted list of keys, one at a time, printing each key.

### 5.4.2 The `values` Function

The `values` function returns, in random order, a list consisting of all the values of a named hash. (After Perl 5.12, it will also return the values of an array.) In scalar context, it returns the number of values.

### FORMAT

```
values (ASSOC_ARRAY)
values ASSOC_ARRAY
```

### EXAMPLE 5.45

(In Script)

```perl
use warnings;

# The values function returns the values in a hash
1 my %weekday= {
    '1'=>'Monday',
    '2'=>'Tuesday',
    '3'=>'Wednesday',
    '4'=>'Thursday',
    '5'=>'Friday',
    '6'=>'Saturday',
    '7'=>'Sunday',
};
2 foreach my $val ( values(%weekday) ){
    print "$val\n";
}
```

(Output)

```
2 Saturday Thursday Monday Wednesday Sunday Tuesday Friday
```

### EXPLANATION

-   1. The hash `%weekday` is assigned keys and values.
-   2. The `values` function returns a list of values from the hash `%weekday`. The `foreach` is used to loop through the list of values, one at a time, using `$val` as its loop variable.

Since hashes are stored in a random order, to get the hash values in the order in which they were assigned, you can use a hash slice as shown in the following example.

### EXAMPLE 5.46

(In Script)

```perl
use warnings;

# Use a hash slice to get the values returned in order.
1 my %weekday= {
    '1'=>'Monday',
    '2'=>'Tuesday',
    '3'=>'Wednesday',
    '4'=>'Thursday',
    '5'=>'Friday',
    '6'=>'Saturday',
    '7'=>'Sunday',
};
