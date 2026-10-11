126

# FORMAT

```
keys (ASSOC_ARRAY)
keys ASSOC_ARRAY
```

# EXAMPLE 5.44

(In Script)

```
use warnings;
my(%weekday, @daynumber, $key);
# The keys function returns the keys of a hash
1 my @weekday= (
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
(Output)
6 4 1 3 7 2 5
6 4 1 3 7 2 5
1 2 3 4 5 6 7
```

# EXPLANATION

+   1. The hash `$weekday` is assigned keys and values.
+   2. The `keys` function returns a list of all the keys in a hash. In this example, `@daynumber` is an unordered list of all the keys in the `$weekday` hash.
+   4. The `keys` function returns a list of keys. The `foreach` loop will traverse the list of keys, one at a time, printing the keys.
+   5. The `keys` function returns a list of keys in `$weekday` hash. The list will then be sorted, and finally the `foreach` loop will traverse the sorted list of keys, one at a time, printing each key.

# 5.4.2 The values Function

The `values` function returns, in random order, a list consisting of all the values of a named hash. (After Perl 5.12, it will also return the values of an array.) In scalar context, it returns the number of values.

7