The general rules for primitive assignment conversion can be stated as follows:

+   * A boolean cannot be converted to any other type.
* A non-boolean can be converted to another non-boolean type, provided the conversion is a widening conversion.
* A non-boolean cannot be converted to another non-boolean type if the conversion would be a narrowing conversion.

Widening conversions change a value to a type that accommodates a wider range than the original. In most cases, the new type has more bits than the original and can be visualized as "wider" than the original, as shown in Figure 4.2.
Widening conversions do not lose information about the magnitude of a value. In the first example in this section, an int value was assigned to a double variable. This conversion was legal because doubles are wider (represented by more bits) than ints, so there is room in a double to accommodate the information in an int. Java's widening conversions are

+   * From a byte to a short, an int, a long, a float, or a double
* From a short to an int, a long, a float, or a double
* From a char to an int, a long, a float, or a double
* From an int to a long, a float, or a double
* From a long to a float or a double
* From a float to a double

Figure 4.3 illustrates all the widening conversions. The arrows can be taken to mean "can be widened to." To determine whether it is legal to convert from one type to another, find the desired type in the figure and see if you can reach the desired type by following the arrows.

# FIGURE 4.2 Widening conversion of a positive value

| XXXX... | |
|---||
| 0 | ... | 0 | XXXX... |