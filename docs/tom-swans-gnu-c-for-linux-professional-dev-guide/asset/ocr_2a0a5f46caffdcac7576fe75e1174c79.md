In this case, the two pairs of iterators could be reversed with the same results placed in colors4. If colors1 equals the set {Orange, Red} and colors3 equals {Blue, Indigo, Violet}, their union in colors4 equals {Blue, Indigo, Orange, Red, Violet}. The source sets must be ordered (by sorting, for example). However, the result is automatically maintained in order.

> Tip
> Use the set container to automatically maintain objects in a specified order. When using a list or other container as a set, it is your responsibility to maintain object order.

To form the intersection of two sets, call the set_intersection() algorithm. For the demonstration, the sample program creates another set to hold the results of the operation:

```
TSet colors5(max(colors1.size(), colors2.size()));
```

Just for the sake of being different, I used the max() algorithm to create a new container of a size equal to colors1 or colors2, whichever is larger. To find the intersection of the two sets—all values in the one set that are also members of the other—the program calls set_intersection():

```
set_intersection(
    colors1.begin(), colors1.end(),
    colors2.begin(), colors2.end(), colors5.begin());
```

Given that colors1 equals the set {Orange, Red} and that colors2 equals {Green, Orange, Red, Yellow}, their intersection in colors5 is the set of common values {Orange, Red}. To find the difference between two sets, the program defines one more container as

```
TSet colors6(colors2.size());
```

The results can be no larger than the second set, so we simply use its size to create the new container. The program finds the difference between colors1 and colors2 using the following statement:

```
set_difference(
    colors2.begin(), colors2.end(),
    colors1.begin(), colors1.end(), colors6.begin());
```

Given the preceding color sets, that statement assigns to colors6 the values {Green, Yellow}—all the values in colors2 that are not members of colors1. When calling set_difference(), the order of the first two pairs of iterators is critical—the algorithm finds the elements in the first range that are not members of the second. Use set_symmetric_difference() to find the dissimilar elements in two sets regardless of order.