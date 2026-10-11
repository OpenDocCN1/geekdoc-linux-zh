# 5.3  Array Functions

Arrays can grow and shrink. The Perl array functions allow you to insert or delete elements of the array from the front, middle, or end of the list, to sort arrays, perform calculations on elements, to search for patterns, and more.

# 5.3.1  Adding Elements to an Array

The push function. The push function pushes values onto the end of an array, thereby increasing the length of the array (see Figure 5.5).

```
FORMAT
push(ARRAY, LIST)
```

```
EXAMPLE 5.22

(In Script)

use warnings;
# Adding elements to the end of a list
my @names = ("Bob", "Dan", "Tom", "Guy");
push(@names, "Jim", "Joseph", "Archie");
print "@names \n";

(Output)
Bob Dan Tom Guy Jim Joseph Archie
```

+   EXPLANATION
+   1. The array @names is assigned list values.
+   2. The push function pushes three more elements onto the end of the array.
+   3. The new array has three more elements appended to it.

![](bbox=[0.0, 0.65, 0.79, 0.94])