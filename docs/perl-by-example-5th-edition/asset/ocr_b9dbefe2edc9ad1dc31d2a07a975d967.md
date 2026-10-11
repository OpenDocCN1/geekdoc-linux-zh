# 6.3 Precedence and Associativity

**String.** The string equality operators evaluate their operands (strings) by comparing the ASCII value of each character in the first string with the corresponding character in the second string. The comparison includes trailing whitespace.

If the first string contains a character that is of a higher ASCII value than the corresponding character in the second string, the value 1 is returned; if the strings are equal, 0 is returned; if the first string character has a lesser ASCII value than the corresponding character in the second string, -1 is returned (see Table 6.7).

| Operator | Example | Meaning |
| :--- | :--- | :--- |
| eq | $Str1 eq $Str2 | $Str1 is equal to $Str2 |
| ne | $Str1 ne $Str2 | $Str1 is not equal to $Str2 |
| cmp | $Str1 cmp $Str2 | $Str1 is compared to $Str2, with a signed return |


```
(The Script)
```perl
use warnings;

1  $Str1 = "A";
   $Str2 = "C";
   $result = $Str1 eq $Str2;
   print "$result\n";

2  $result = $Str1 ne $Str2;
   print "$result\n";

3  $result = $Str1 cmp $Str2;
   print "$result\n";

4  $result = $Str2 cmp $Str1;
   print "$result\n";

5  $Str1 = "C";       # Now both strings are equal
6  $result = $Str1 cmp $Str2;
   print "$result\n";

(Output)
1
2   1
3   -1
4    1
6    0
```
```