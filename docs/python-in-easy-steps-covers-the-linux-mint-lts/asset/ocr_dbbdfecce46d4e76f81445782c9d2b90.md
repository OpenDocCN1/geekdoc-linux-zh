references the second element in the example above – not the first element, as element numbering starts at zero.

[0]   [1]   [2]
[0]   1     2     3
[1]   4     5     6

Lists can have more than one index – to represent multiple dimensions, rather than the single dimension of a regular list. Multi-dimensional lists of three indices and more are uncommon, but two-dimensional lists are useful to store grid-based information such as X,Y coordinates.

A list of string values can even be considered to be a multi-dimensional list, as each string is itself a list of characters. So each character can be referenced by its index number within its particular string.

+   1. Start a new Python script by initializing a list of three elements containing string values
+       `quarter = ['January', 'February', 'March']`

+   2. Next, add statements to individually display the value contained in each list element
+       `print('First Month :', quarter[0])`
+       `print('Second Month :', quarter[1])`
+       `print('Third Month :', quarter[2])`

+   3. Add a statement to create a multi-dimensional list of two elements, which themselves are lists that each have three elements containing integer values
+       `coords = [[1,2,3],[4,5,6]]`

+   4. Now, add statements to display the values contained in two specific inner list elements
+       `print('Top Left 0,0 :', coords[0][0])`
+       `print('Bottom Right 1,2 :', coords[1][2])`