An array has the same kind of naming conventions as a scalar variable, except that it begins with an `at` sign (`@`) instead of a dollar sign. As these examples show, an array does not need to be declared with a certain size or contain only a consistent type of data. Arrays can contain numbers, strings, other arrays, or whatever you like.

You can access an element of an array using square brackets. The third element of the previous `@array1` array, a scalar value, would be `$array1[2]`. Remember that array element numbering begins at zero!

You will also see elements of arrays addressed with the `@` prefix instead of `$`. This prefix indicates that you can address a "slice" of an array by specifying more than one element (for example, `@array1[1,2]`). This example is really an array in itself with two elements. If you say `@array1[2]`, you're talking about a slice with one element, which is effectively the same thing as a scalar variable, and it works the same way. However, for consistency's sake, you may want to keep in mind that the "preferred" method is `$array1[2]`.

You can use the various array operators, essentially built-in functions, to set up your arrays in any way you like. Arrays are often also called *lists*. In that context, you can think of an array in `"stack"` terminology, which gives you the `push()`, `pop()`, `shift()`, and `unshift()` operators. These operators are listed in Table 20.2, where `@array1` undergoes each of them in turn.

# TABLE 20.2 List Operators

| Operator | Function Result | Syntax |
| :--- | :--- | :--- |
| `push()` | Adds a value to the end of a list. | `push(@array1, "test"); @array1 = ("blah",5,12,7,6,"test")` |
| `pop()` | Removes a value from the end of a list and returns it. | `$d = pop(@array1); @array1 = ("blah",5,12,7,6), $d = "test"` |
| `unshift()` | Adds a value to the beginning of a list. | `unshift(@array1, "test"); @array1 = ("test","blah",5,12,7,6)` |
| `shift()` | Removes a value from the beginning of a list and returns it. | `$d = shift(@array1); @array1 = ("blah",5,12,7,6), $d = "test"` |

> TIP
> You can accomplish each of these operations by setting the output of the operator to a new array, or even to the same array. Therefore, by writing `@array3 = push(@array1,"test")`, you can create a new array with the new lengthened contents, leaving the original array (`@array1`) untouched.

A further useful array function is `sort()`. For instance, `sort(@array1)` would arrange all the elements in lexicographical order, treating them as strings. You can specify an alternate sorting algorithm of your own construction to extend the functionality of the `sort()`