**Output:**
Y = (0.0, 2.0, 0.0, 0.0, 6.0, 10.0, 0.0, 8.0, 9.0, 0.0)
X = (7.0, 4.0, 6.0, 0.0, -2.0)

# ### Example 3

This example shows how to use CGTHRZ to copy specified elements of a vector $y$ into a sparse vector $x$ of length 3, where the elements of array INDEX are in random order.

**Call Statement and Input:**
NZ Y X INDEX
| | | |
CALL CGTHRZ( 3 , Y , X , INDEX )
Y = ((6.0, 5.0), (-2.0, 3.0), (15.0, 4.0), (9.0, 0.0))
INDEX = (4, 1, 3)

**Output:**
Y = ((0.0, 0.0), (-2.0, 3.0), (0.0, 0.0), (0.0, 0.0))
X = ((9.0, 0.0), (6.0, 5.0), (15.0, 4.0))