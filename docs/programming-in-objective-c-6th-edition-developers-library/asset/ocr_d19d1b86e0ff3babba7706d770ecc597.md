# **Working with Unions**

One of the more unusual constructs in the C programming language is the union. This construct is used mainly in more advanced programming applications in which it is necessary to store different types of data in the same storage area. For example, if you want to define a single variable called x, which could be used to store a single character, a floating-point number, or an integer, you could first define a union called, perhaps, m

```
u
{

}

```

The declaration for a union is identical to that of a structure, except the keyword u is used where the keyword s is otherwise specified. The real difference between structures and unions has to do with the way memory is allocated. Declaring a variable to be of type u m, as in

```
u
```

does not define x to contain three distinct members called c, f, and i; rather, it defines x to contain a single member that is called either c, f, or i. In this way, the variable x can be used to store either a c or a f or an i, but not all three (or not even two of the three). You can store a character in the variable x with the following statement:

```
x
```

The character stored in x can subsequently be retrieved in the same manner. So, to display its value at the terminal, for example, the following could be used:

```
p
```

To store a floating-point value in x, the notation x is used:

```
x
```

Finally, to store the result of dividing an integer c by 2 in x, the following statement can be used:

```
x
```

Because the f, c, and i members of x all exist in the same place in memory, only one value can be stored in x at a time. Furthermore, it is your responsibility to ensure that the value retrieved from a union is consistent with the way it was last stored in the union.

A union member follows the same rules of arithmetic as the type of the member that is used in the expression. So in

```
x
```

the expression is evaluated according to the rules of integer arithmetic because x and 2 are both integers.

A union can be defined to contain as many members as desired. The C compiler ensures that enough storage is allocated to accommodate the largest member of the union. Structures can be defined that contain unions, as can arrays. When defining a union, the name of the union is not required, and