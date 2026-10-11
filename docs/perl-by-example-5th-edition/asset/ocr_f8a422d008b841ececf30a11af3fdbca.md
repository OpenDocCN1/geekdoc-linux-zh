# G.2 Scalars, Arrays, and Hashes

# EXPLANATION (CONTINUED)

+   4	The array @items is initialized with the values of three scalar variables.

+   5	The array @empty is assigned an empty list.

+   6	The array @items is assigned to the scalar variable $size. The value of the scalar is the number of elements in the array (in this example, 3).

+   7	The qw (quote word) construct is followed by a delimiter of your choice and a string qw@) extracts words out of your string using embedded whitespace as the delimiter and returns the words as a list. Variables are not interpolated. Each word in the list is treated as a singly quoted string. The list is terminated with a closing delimiter. This example could be written like so:
+   
+       @animals = ('cats', 'dogs', 'owls');

+   8	The qw construct accepts paired characters (), {}, [], and [], as optional delimiters.

**Output and Input Special Variables ($, and $/).** The $, is a special default global variable, called the output field separator. When used with the print function to print a list or an array (not enclosed in quotes), this variable separates the elements and is initially set to undef. For example, print 1,2,3 would output 123. Although you can assign a different value to the $, it's not a good idea, as once changed, it will affect your whole program. (The join function would provide a better solution.)

# EXAMPLE 5.11

```
1 use warnings;
2 my @pets=("Smokey", "Fido", "Gillsa", "Skiddy");
3 print @pets, "\n";  # Output separator is undef
4 $_,="*****";  # Changes the output field separator
5 print @pets, "\n";  # no quotes; ***** replaces undef
6 print 1,2,3, "\n";
```

(Output):
SmokexPidoxGillaxSkiddy
Smokey*****Fido*****Gillsa*****Skiddy*****
1****2***3*****

# EXPLANATION

+   3	The array of pets is printed. The value of $, is used to separate elements of an un-quoted list for the print function and is initially set to undef.

+   4	The $, variable is reset to "*****".

+   5	Now, when the print function displays an unquoted list, the list items are separated by that string.

+   6	The comma evaluates to "*****" in the print function.

The $" is a special scalar variable, called the list separator, used to separate the elements of a list in a string, and is by default a single space. For example, when you print an array enclosed in double quotes, the value of $" will be preserved, and you will have a space between the elements.