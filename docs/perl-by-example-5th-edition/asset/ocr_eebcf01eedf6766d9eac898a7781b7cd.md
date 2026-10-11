Since reserved words and filehandles are not preceded by a special character, variable names will not conflict with its left-hand side. Names are **case sensitive**. The variables named $Num, $num, and $NUM are all different. If a variable starts with a letter, it may consist of any number of letters (an underscore counts as a letter) and/or digits. If the variable does not start with a letter, it must consist of only one character. Perl has a set of special variables (for example, `$_`, `$*`, `$!`, `$1, $2`) that fall into this category. (See Section A.2, “Special Variables,” in Appendix A.) In special cases, variables may also be preceded with a single quote, but only when packages are used. An uninitialized variable will get a value of zero or undef, depending on whether its context is numeric or string.

# ### 5.1.4 Assignment Statements

The assignment operator, the equal sign (=), is used to assign the value on its right-hand side to a variable on its left-hand side. Any value that can be “assigned to” represents a named region of storage and is called an *value*.<sup>2</sup> Perl reports an error if the operand on the left-hand side of the assignment operator does not represent an *value*.

When assigning a value or values to a variable, if the variable on the left-hand side of the equal sign is a scalar, Perl evaluates the expression on the right-hand side in a scalar context. If the variable on the left of the equal sign is an array, then Perl evaluates the expression on the right in an array or list context (see Section 5.2, “Scalars, Arrays, and Hashes”).

**EXAMPLE 5.3**

```
(The Script)
use warnings;
# Scalar, array, and hash assignment
my $salary=50000;             # Scalar assignment
my @months=('Mar', 'Apr', 'May');  # Array assignment
my %states= (
  CA => 'California',
  ME => 'Maine',
  MT => 'Montana',
  NM => 'New Mexico',
);

print "$salary";
print "@months";
print "$months[0], $months[1], $months[2]\n";
print "${states{CA}}, ${states{NM}}"\n";
print $x + 3, "\n";              # $x just came to life!
print "***$name***"\n";          # $name is born!
```

+   2. The value on the left-hand side of the equal sign is called an *value*, and the value on the right-hand side is called an *value*.