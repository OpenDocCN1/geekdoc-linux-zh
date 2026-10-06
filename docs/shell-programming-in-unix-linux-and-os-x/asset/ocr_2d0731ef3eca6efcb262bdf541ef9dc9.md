# The printf Command 205

As you can see, using + or space as the flag causes a column of positive and negative numbers to align nicely.

The width modifier is a positive number that specifies the minimum field width for printing the argument. The argument is right-justified within this field unless the flag is used:

```
$ printf "%02d\n" string1 string2
string1 string2
$ printf "-%2d-%02d\n" string1 string2
string1 string2
$ printf "%5d%%5d\n" 1 10 100
$ printf "-%5d%%5d\n" -1 -10 -100
$ printf "%-5d%%5d\n" 1 10 100
10 100
$
```

The width can be useful for lining up columns of text or numbers (Tip: for numbers and leading 0, %x, and %X characters are counted as part of the argument width). The width specifies a minimum size for the field, but if the width of an argument exceeds width, it can overflow or not be output at all. An easy way to test:

```
printf "-%15.15s\n"this is more than 15 chars long"
```

What happens on your system when you command that?

The .precision is a positive number that specifies a minimum number of digits to be displayed for %d, %u, %o, %x, and %X. This results in zero-padding on the left of the value:

```
$ printf "%5d.%4X\n" 10 27
00010 01B
$
```

For strings, the .precision modifier specifies the maximum number of characters to be printed from the string. If the string is longer than precision characters, it is truncated on the right. It's important to realize as you line up across multiple lines, but with some data missing if any individual value is wider than the field:

```
$ printf "%6s\n" "Ann Smith"
Ann Sm
$
```

A width can be combined with .precision to specify both a width and zero padding (for numbers) or truncation (for strings):

```
$ printf "%:%10.5x%%5.4x%%5.4d\n" 1 10 100
000001: 000a
$ printf "%:%9.5s\n" abcdef
:abcde
$ printf ":%9-9.5s\n" abcdef
:abcde
$
```