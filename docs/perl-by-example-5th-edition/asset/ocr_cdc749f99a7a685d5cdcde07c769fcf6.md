When you have a collection of similar data elements, it is easier to use an array than to create a separate variable for each of the elements. The array name allows you to associate a single variable name with a list of data elements. Each of the elements in the list is referenced by its name and a subscript (also called an **index**).

Perl, unlike C-like languages, doesn't care whether the elements of an array are of the same data type. They can be a mix of numbers and strings. To Perl, an **array is a list containing an ordered set of scalars**. The name of the array starts with an @ sign and the list is enclosed in parentheses; each element assigned an index value starting at zero (see Figure 5.2).

**Assignment**. If the array is initialized, the elements are enclosed in parentheses, and each element is separated by a comma. The list is parenthesized due to the lower precedence of the comma operator over the assignment operator. Elements in an array are simply scalars.

The `qw` construct can also be used to quote words in a list (similar to `qq`, `q`, and `qx`). The items in the list are treated as singly quoted words and the comma is also provided.

```
$pal = "John"; # Scalar holds one value
@pals = ("John", "Sam", "Nicky", "Jake" ); # Array holds a list of values
@pals = qw(John Sam Nicky Jake); # qw means quote word and include comma
```

![](bbox=[0.11, 0.5, 0.91, 0.62])

![](bbox=[0.18, 0.59, 0.31, 0.61])

![](bbox=[0.6, 0.59, 0.69, 0.61])

**Figure 5.2** A scalar variable and an array variable.

# EXAMPLE 5.10

```
1 @name=("Guy", "Tom", "Dan", "Roy");
2 @list=(2..10);
3 @grades=(100, 90, 65, 96, 40, 75);
4 @items=(Sa, Sb, Sc);
5 @empty=();
6 @size=@items;
7 @animals = qw(dogs cats cows);
8 @fruit = qw(apples pears peaches);
```

# EXPLANATION

1 The array @name is initialized with a list of four string literals.

2 The array @list is assigned numbers ranging from 2 through 10.

3 The array @grades is initialized with a list of six numeric literals.