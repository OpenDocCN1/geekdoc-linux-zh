long, whereas a *short* int has a minimum size of only 2 bytes. The size of an *int* is system dependent, but it definitely is at least as large as a *short*.

The *unsigned* qualifier is reserved for *int* and *char* types only. Normally, each of these types holds negative as well as positive values. This qualifier is the default signed form of these data types. You can use the *unsigned* qualifier when you want the variable to hold positive values only. Here are some examples of using the *short, long*, and *unsigned* qualifiers:

```
```
unsigned char mode_select, printer_status;
short     record_number;        /* Same as 'short int' */
long      offset;               /* Same as 'long int' */
unsigned  i, j, msg_id;        /* Same as 'unsigned int' */
unsigned short width, height;   /* Same as 'unsigned short int' */
unsigned long file_pos;         /* Same as 'unsigned long int' */
long double result;
```
```

When the *short, long*, and *unsigned* qualifiers are used with *int* types, you can drop the *int* from the declaration. You can also extend the *double* data type with a *long* prefix.

![](bbox=[0.14, 0.46, 0.22, 0.56])

GCC comes with the predefined header files --- *limits.h* and *float.h* --- that define exact sizes of the various data types --- and ranges of values --- in those header files. You can examine these files in the */usr/include* directory of your Linux system to determine the sizes of the basic data types that the GCC compiler supports.

# ### Enumerations

You can use the *enum* data type to define your own enumerated list --- a fixed set of named integer constants. For example, you can declare a Boolean data type named *BOOLEAN* by using *enum* as follows:

```
```
/* Declare an enumerated type named BOOLEAN */
enum BOOLEAN {false = 0, true = 1, stop = 0, go = 1,
              off = 0, on = 1};
/* Define a BOOLEAN called "status" and initialize it */
enum BOOLEAN status = stop;
```
```

This example first declares *BOOLEAN* to be an enumerated type. The list within the braces shows the enumeration constants that are valid values of an *enum* *BOOLEAN* variable. You can initialize each constant to a value of your choice, and several constants can use the same value. In this example, the constants *false, stop*, and *off* are set to 0, while *true, go*, and *on* are initialized to 1. The example then defines an enumerated *BOOLEAN* variable named *status*, which is initially set to the constant *stop*.