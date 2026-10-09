statements displays three values, using commas to separate them within the `print` statement. The second `print` statement has one argument and demonstrates that Perl expands a variable (replaces the variable with its value) when the variable is enclosed within double quotation marks.

**$array** The final `print` statement in `arrayvar2.pl` shows that Perl evaluates the variable `$array` as the index of the last element in the array named `array`. Because Perl uses zero-based indexing by default, this variable evaluates to one less (i., the number of elements in the array.

The next example works with elements of an array and uses a dot (., the string concatenation operator). The first two lines assign values to four scalar variables. The third line shows that you can assign values to array elements using scalar variables, arithmetic, and concatenated strings. The dot operator concatenates strings, so Perl evaluates `$va . $vb` as `Sam` concatenated with `uel`—that is, as `Samuel` (see the output of the last `print` statement).

```
```
$ cat arrayvar3.pl
#!/usr/bin/perl -w
$vl = 5; $v2 = 8;
$va = "Sam"; $vb = "uel";
@arrayvar3 = ($vl, $vl * 2, $vl * $v2, "Max", "Zach", $va . $vb);

print $arrayvar3[2], "\n";        # one element of an array is a scalar
print @arrayvar3[2,4], "\n";      # two elements of an array are a list
print @arrayvar3[2..4], "\n\n";   # a slice

print "@arrayvar3[2,4]", "\n";      # a list, elements separated by SPACes
print "@arrayvar3[2..4]", "\n\n";    # a slice, elements separated by SPACeS

print "@arrayvar3\n";               # an array, elements separated by SPACes

$ ./arrayvar3.pl
40
40Zach
40MaxZach

40 Zach
40 Max Zach

5 10 40 Max Zach Samuel
```
```

The first `print` statement in `arrayvar3.pl` displays the third element (the element with an index of 2) of the `@arrayvar3` array. This statement uses $ in place of @ because it refers to a single element of the array. The subsequent `print` statements use @ because they refer to more than one element. Within the brackets that specify an array subscript, two subscripts separated by a comma specify two elements of an array. The second `print` statement, for example, displays the third and fifth elements of the array.