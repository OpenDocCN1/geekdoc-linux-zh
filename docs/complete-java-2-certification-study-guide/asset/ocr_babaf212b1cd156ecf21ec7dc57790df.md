# FIGURE 4.3 Widening conversions

![](bbox=[0.233, 0.143, 0.858, 0.246])

The figure shows, for example, that it is perfectly legal to assign a byte value to a float variable, because you can trace a path from byte to float by following the arrows (byte to short to int to long). You cannot, on the other hand, trace a path from long to short, so it is not legal to assign a long value to a short variable.

Figure 4.3 is easy to memorize. The figure consists mostly of the numeric data types in size of a 16-bit char “fits inside” a 32-bit int (Note that you can’t convert a byte to a char or a char to short, even though it seems reasonable to do).

Any conversion between primitive types that is not represented by a path of arrows in Figure 4.3 is a narrowing conversion. These conversions lose information about the magnitude of the value being converted and are not allowed in assignments. impossible to portray the narrowing conversions in a diagram like Figure 4.3, but they can be summarized as:

+   * From a byte to a char
* From a short to a byte or a char
* From a char to a byte or a short
* From an int to a byte, a short, or a char
* From a long to a byte, a short, a char, or an int
* From a float to a byte, a short, a char, an int, or a long
* From a double to a byte, a short, a char, an int, a long, or a float

You do not really need to memorize this list. It simply represents all the conversions not shown in Figure 4.3, which is easy to memorize.

# Assignment Conversion, Narrower Primitives, and Literal Values

Java’s assignment rule is sometimes inconvenient when a literal value is assigned to a primitive. By default, a numeric literal is either a double or an int, so the following line of code generates a compiler error:

```
float f = 1.234;
```

The literal value 1.234 is a double, so it cannot be assigned to a float variable.