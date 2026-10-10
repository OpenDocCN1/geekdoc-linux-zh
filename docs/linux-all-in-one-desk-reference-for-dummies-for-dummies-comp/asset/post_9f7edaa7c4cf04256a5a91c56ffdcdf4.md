
The characters in the string array occupy successive storage locations, beginning with location 0. Thus in this example, *string*[0] refers to the first character in this array, while *string*[79] refers to the last one. You can define arrays of other data types and structures similarly:

```
struct Customer          /* Declare a structure   */
{
    int id;
    char first_name[40];
    char last_name[40];
};
struct Customer customers[100]; /* Define array of structures */
int                index[64];   /* An array of 64 integers   */
```

You can also define multidimensional arrays. For example, to represent an 80-column-by-25-line text-display screen, you can use a two-dimensional array as follows:

```
unsigned char text_screen[25][80];
```

Each item of *text_screen* is an array of 80 *unsigned chars*, and *text_screen* contains 25 such arrays. In other words, the two-dimensional array is stored by laying out one row after another in memory. You can use expressions such as *text_screen*[0] [0] to refer to the first character in the first row and *text_screen*[24] [79] to refer to the last character of the last row of the display screen. Higher-dimensional arrays are defined similarly:

```
float coords[3][2][5];
```

This example defines *coords* as a three-dimensional array of three data items: Each item is an array of two arrays, each of which, in turn, is an array of five *float* variables. Thus, you interpret a multidimensional array as an *array of arrays*.

## Pointers

A *pointer* is a variable that can hold the address of any type of data except a bit field. For example, if *p_i* is a pointer to an integer variable, you can define and use it as follows:

```
/* Define an int pointer and an integer */
int *p_i, count;
/* Set pointer to the address of the integer "count" */
p_i = &count;
```

In this case, the compiler allocates storage for an *int* variable *count* and a pointer to an integer *p_i*. The number of bytes necessary to represent a pointer depends on the underlying system's addressing scheme.

Don't use a pointer until it contains the address of a valid object.

The example shows `p_i` being initialized to the address of the integer variable count using the `&` operator, which provides the address of a variable. After `p_i` is initialized, you can refer to the value of `count` with the expression `*p_i`, which is read as “the contents of the object with its address in `p_i`.”

Pointers are useful in many situations; an important one is the dynamic allocation of memory. The standard C libraries include functions such as `malloc` and `calloc`, which you can call to allocate storage for arrays of objects. After allocating memory, these functions return the starting address of the block of memory. Because this address is the only way to reach that memory, you must store it in a variable capable of holding an address — a pointer.

Suppose that you allocated memory for an array of 50 integers and saved the returned address in `p_i`. Now you can treat this block of memory as an array of 50 integers with the name `p_i`. Thus, you can refer to the last element in the array as `p_i[49]`, which is equivalent to `*(p_i+49)`. Similarly, C treats the name of an array as a pointer to the first element of the array. The difference between the name of an array and a pointer variable is that the name of the array is a constant without any explicit storage necessary to hold the address of the array’s first element. The pointer, on the other hand, is an actual storage location capable of holding the address of any data.

In addition to storing the address of dynamically allocated memory, pointers are also commonly used as arguments to functions. When a C function is called, all of its arguments are passed by value — that is, the function gets a copy of each argument, not the original variables appearing in the argument list of the function call. Thus, a C function cannot alter the value of its arguments. Pointers provide a way out. To change the value of a variable in a function, you can pass a pointer to the variable; the function can then alter the value through the pointer.

## Structures, Unions, and Bit Fields

### Type definitions

Through the `typedef` keyword, C provides you with a convenient way of assigning a new name to an existing data type. You can use the `typedef` facility to give meaningful names to data types used in a particular application. For example, a graphics application might declare a data type named `Point` as follows:

```c
/* Declare a Point data type */
typedef struct Point
{
    short x;
    short y;
} Point;
```

![](img/11709a8f88c8cd03868a929dc94c0e2b_734_0.png)

```
/* Declare PointPtr to be pointer to Point types */
typedef Point *PointPtr;
/* Define some instances of these types
 * and initialize them */
Point      a = {0, 0};
PointPtr   p_a = &a;
```

As shown by the `Point` and `PointPtr` types, you can use `typedef` to declare complex data types conveniently.

### Type qualifiers: const and volatile

Two type qualifiers, `const` and `volatile`, work this way in a declaration:

- The `const` qualifier in a declaration tells the compiler that the program must not modify the particular data object. The compiler must not generate code that might alter the contents of the location where that data item is stored.
- The `volatile` qualifier specifies that factors beyond the program’s control may change the value of a variable.

You can use both `const` and `volatile` keywords on a single data item to mean that, although your program must not modify the item, some other process may alter it. The `const` and `volatile` keywords always qualify the item that immediately follows (to the right). The information provided by the `const` and the `volatile` qualifiers is supposed to help the compiler optimize the code it generates. For example, suppose that the variable `block_size` is declared and initialized as follows:

```
const int block_size = 512;
```

In this case, the compiler does not need to generate code to load the value of `block_size` from memory. Instead, it can use the value 512 wherever your program uses `block_size`. Now suppose that you add `volatile` to the declaration and change the declaration to

```
volatile const int block_size = 512;
```

This declaration says that some external process can change the contents of `block_size`. Therefore, the compiler cannot optimize away any reference to `block_size`. You may need to use such declarations when referring to an I/O port or video memory because these locations can be changed by factors beyond your program’s control.

## Expressions

An *expression* is a combination of variables, function calls, and operators that results in a single value. For example, here is an expression with a value that is the number of bytes needed to store the *null-terminated string* `str` (that is, an array of char data types with a zero byte at the end):

```
(strlen(str) * sizeof(char) + 1)
```

This expression involves a function call — `strlen(str)` — and the multiplication (*), addition (+), and `sizeof` operators.

C has a large number of operators that are an important part of expressions. Table 2-2 provides a summary of the operators in C.

**Table 2-2 Summary of C Operators**

| Name of Operator | Syntax | Result |
| :--- | :--- | :--- |
| **Arithmetic Operators** | | |
| Addition | x+y | Adds x and y |
| Subtraction | x-y | Subtracts y from x |
| Multiplication | x*y | Multiplies x and y |
| Division | x/y | Divides x by y |
| Remainder | x%y | Computes the remainder that results from dividing x by y |
| Preincrement | ++x | Increments x before use |
| Postincrement | x++ | Increments x after use |
| Predecrement | --x | Decrements x before use |
| Postdecrement | x-- | Decrements x after use |
| Minus | -x | Negates the value of x |
| Plus | +x | Maintains the value of x unchanged |
| **Relational and Logical Operators** | | |
| Greater than | x>y | Value is 1 if x exceeds y; otherwise, value is 0. |
| Greater than or equal to | x>=y | Value is 1 if x exceeds or equals y; otherwise, value is 0. |
| Less than | x<y | Value is 1 if y exceeds x; otherwise, value is 0. |
| Less than or equal to | x<=y | Value is 1 if y exceeds or equals x; otherwise, value is 0. |

(continued)

**Expressions** 711

**Book VIII**
Chapter 2

**Programming in C**
