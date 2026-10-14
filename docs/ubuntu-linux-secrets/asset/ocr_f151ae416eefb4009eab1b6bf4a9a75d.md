The data value in hashes follows the same format as scalar data values. You can store text string, integer, or floating point values in the hash data. Similar to the array, you can refer to an individual data value in a hash using the key. The format is slightly different from the method used for arrays, though:

`$hash{key}`

The key is a text string representing the specific element in the hash, and is enclosed in braces. Also unlike arrays that have incremental numerical indexes, the hash keys don’t have any set values. You can use any type of string value as a key:

```
```perl
$ cat test5.pl
#!/usr/bin/perl
# testing hash variables
%favorites = ("fruit" => "banana", "vegetable" => "carrot");
print "My favorite fruit is $favorites{'fruit'}\n";
$ chmod +x test5.pl
$ ./test5.pl
My favorite fruit is banana
$
```
```

This works just fine when you're looking for a specific key value, but it can make trying to iterate through a hash variable that contains unknown keys somewhat tricky.

Fortunately, Perl provides two handy functions to help determine what's inside a hash variable:

+   - **keys**: returns an array containing the key values in the hash
+   - **values**: returns an array containing the values in the hash

The keys function allows us to retrieve the individual key values so we can iterate through them, even though we might not know what they are. The best way to process keys in an array is with the `foreach` statement.

The `foreach` statement iterates through a set of statements for each element in the defined array. Here's a sample program that uses the `foreach` statement to iterate through the keys in a hash variable:

```
```perl
$ cat test6.pl
#!/usr/bin/perl
# more testing of hash variables
%favorites = ("fruit" => "banana", "vegetable" => "carrot");

foreach $key (keys %favorites)
{
print "My favorite $key is $favorites{$key}\n";
}
$ chmod +x test6.pl
$ ./test6.pl
My favorite fruit is banana
My favorite vegetable is carrot
$
```
```

In each iteration, the `foreach` statement assigns the next key in the `%favorites` hash to the `$key` variable. When there aren't any more keys, the `foreach` statement stops. Notice