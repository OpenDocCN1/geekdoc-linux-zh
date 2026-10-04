# Tutorial Introduction to Ada

The operator ** is Ada's exponentiation operator. Here, we are using it to square values. If we want our function to work, we also need to add the following lines to the file geometry.ada.

![](bbox=[0.065, 0.165, 0.195, 0.665])

```
with Ada.Numerics.Element_Functions;
use Ada.Numerics.Element_Functions;
```

This allows us to use the Sqrt function to calculate the square root of a number. Alternatively, it might be a good idea to use the direct selection of the Distance function.

# Instantiate generic packages

It's been a while since we compiled all code, so let's test this. Go back to the tutorial.ada, and add the following line to the top:

+   - Geometry

Since it is a generic package, we cannot use it straight away; we must instantiate it with a particular dimension. The declarative section of the package contains the following lines:

```
procedure Tutorial Geometry_2 is new Geometry(2);
begin
```

The first lines instantiate the generic package; it creates a particular instance of the package, which corresponds to two dimensions. The generic parameter dimension will be set to 2, which means Ada package contains the integers 1 and 2, and Point will be of type Float. When we call a function from that package, we get all the functions and procedures from our package, specifically for 2D geometry.
So let's test it out. Under the "Hello, world", we add a call to Put_Line:

```
Put_Line("Hello, world!");
Put_Line(Float(Distance(0.0, 0.0), (3.0, 4.0)));
```

![](bbox=[0.575, 0.165, 0.875, 0.315])

Generic bodies do not declare generic functions - they are declared in the specification
The two elements (0.0, 0.0) and (3.0, 4.0) are examples of instantiation in Ada. Since Point is the type of arrays with integers 1 and 2, we can create an instance by using the same function type. Float is a type of Integer that we can use to convert integers into strings. We should be able to return integers as well. Our code will give us the following output:

Hello, world!
5.0E+00

> Unlike duplicate, it makes sense to use generics to create one version of the function that we can specialise

Generic procedures
Let's go back to Ada and add a new type, Vector, representing another pair of points. We can do this by using the existing Point type.

Type Point is (Array) of Float; type Vector is New;

Even though these types appear to be the same, it is a good argument to treat them differently. For example, if we want to add two points to a vector or to add two points to a new point, based on our choice of origin, which might be arbitrary. On the other hand, we want to be able to add a vector to a point in order of the operation. We want to make it impossible to perform actions that do not make sense, like adding two points.
We want to add functions that we use to add two vectors to a third vector, and to add a vector to a point to get a second point.

![](bbox=[0.065, 0.745, 0.495, 0.905])