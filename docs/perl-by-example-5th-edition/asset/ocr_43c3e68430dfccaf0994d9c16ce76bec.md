# EXPLANATION

+   1 The array `@grades` is assigned a list of five numbers.
+   2 The `$#` construct gets the index value of the last element in the array.
+   3 By using `$grades` as an index value, the expression would evaluate to `$grades[$#]`.
+   4 The built-in `scalar` function forces the array to be in scalar context and returns the number of elements in the array. You could also assign the array to a scalar variable, as in `$size = @grades`, to produce the same result as shown in line 6.
+   6 Using an empty list causes the array to be completely truncated to an empty list.

**The Range Operator and Array Assignment.** The `..` operator, called the range operator, when used in a list context, returns a list of values starting from the left value to the right value, counting by ones.

# EXAMPLE 5.14

```
use warnings;
my @digits=(0 .. 10);
my @letters= ( 'A' .. 'Z' );
my @alpha= ('A' .. 'Z', 'a' .. 'z');
my @n= (-5 .. 20);
```

# EXPLANATION

+   1 The array `@digits` is assigned a list of numbers, 0 incremented by 1 until 10 is reached.
+   2 The array `@letters` is assigned a list of capital letters, A through Z (ASCII values of A through Z).
+   3 The array `@alpha` is assigned a list of uppercase and lowercase letters.
+   4 The array `@n` is assigned a list of numbers, -5 through 20.

**Accessing Elements.** An array is an ordered list of scalars. To reference the individual elements in an array, each element (a scalar) is preceded by a dollar sign. The index starts at 0, followed by positive whole numbers. For example, in the array `@colors`, the first element in the array is `$colors[0]`, the next element is `$colors[1]`, and so forth. You can also access elements starting at the end of an array with the index value of -1 and continue downward; for example, -2, -3, and so forth.

+   1. To assign a list of values to an array:
+   ```
+   @colors = qw (green red blue yellow);
+   ```
+   2. To print the whole array, use the @:
+   ```
+   print "@colors\n";
+   ```
+   3. To print single elements of the array:
+   ```
+   print "$colors[0] $colors[1]\n";
+   ```