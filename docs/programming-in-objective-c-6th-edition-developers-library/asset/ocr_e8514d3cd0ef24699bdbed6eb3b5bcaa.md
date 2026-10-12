*   stores the value of v in the element pointed to by p and has type t

p   tests if p is pointing to an earlier element in a than is p and has type i (any relational operators can be used to compare two pointers)

p   produces the number of elements in a contained between the pointers p and p (assuming that p points to an element further in a than p ) and has integer type

a   produces a pointer to element number n of a, has type "pointer to t," and is in all ways equivalent to the expression &

*   references element number n of a, has type t, and is in all ways equivalent to the expression a

The actual type of the integer produced by subtracting two pointers is specified by p , which is defined in the standard header file <  .

# **Pointers to Structures2**

> 2. Also applies to unions.

Given that

+   x   is an l value expression of type S S

+   p   is a modifiable lvalue expression of type "pointer to S S"

+   m   is the name of a member of the structure S and is of type t

+   v   is an expression

then the expression

+   &   produces a pointer to x and is of type "pointer to S S"

+   p   sets p pointing to x and is of type "pointer to S S"

+   p