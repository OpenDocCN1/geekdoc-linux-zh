Whichever style you choose, you may assign initial values to variables, or you may leave them uninitialized. (If they are global, however, remember that they are automatically initialized to zero.) The following statement declares four int variables and initializes two of them, v2 and v4, to the values 123 and 321, respectively.

```
int v1, v2 = 123, v3, v4 = 321;
```

That looks jumbled to me, so as a general rule, I use the shorthand declaration style only for uninitialized variables. If I intend to assign initial values, I prefer to write them on separate lines as follows:

```
int v2 = 123;
int v4 = 321;
```

# ENUMERATED TYPES

An enumerated type is a symbolic representation of a series of values such as the colors of the rainbow, the days of the week, or any other series that can be represented in a program using integers. For instance, suppose that you want to represent a rainbow’s seven fundamental colors. To give a name to each color, you could define symbolic constants such as these:

```
#define RED     0
#define ORANGE  1
#define YELLOW  2
#define GREEN   3
#define BLUE    4
#define INDIGO  5
#define VIOLET  6
```

The values are meaningless—they just give the program a convenient way to represent color names as unique integer values that might be stored in variables, written to disk files, or used in other ways. Given these symbols, a program can declare an int variable like this:

```
int color;
```

and then assign to color any of the color symbols:

```
color = GREEN;
```

The compiler replaces GREEN with that symbol’s associated text, in this case the single digit 3. In effect, the statement is compiled as

```
color = 3;
```

Obviously, the symbol GREEN is more meaningful than the literal value 3. But typing a long series of color names and other relatively fixed symbols (the months of the year, for instance) is drudge work. Also, there’s nothing in the program to indicate that the individual color symbols are related.

To make creating such lists easier, C++ provides a helpful device, called an enumerated type. Using the reserved word enum, you can create the preceding seven color constants using a single declaration:

```
enum { RED, ORANGE, YELLOW, GREEN, BLUE, INDIGO, VIOLET };
```