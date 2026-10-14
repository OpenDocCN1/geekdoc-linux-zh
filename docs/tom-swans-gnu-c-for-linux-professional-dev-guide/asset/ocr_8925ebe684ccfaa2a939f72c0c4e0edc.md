The main program starts the recursive ball rolling by calling function A() with the argument 'Z'. Function A() examines its parameter c. If c is alphabetically greater than 'A', the function calls B(), which immediately calls A(), passing c-- as an argument. That causes A() to again examine c, equal to one less than its former value, and then again call B(), until c equals 'A'. At this point, the recursion unwinds, executing the output statement 26 times, and displaying the alphabet, one character at a time. Okay, you can laugh now.

Tip

Walk through onfirst.cpp using the GNU debugger's next and step commands to see how it works in slow motion.

# FUNCTIONS AND SEPARATE COMPILATION

It's often useful to compile functions in separate modules, an especially valuable technique for creating function libraries that multiple programs can share. To illustrate, the following listings create a modular version of the kilo.cpp program in this chapter. Listing 10.12, kilos.h, is a header file with a single element: the kilos() function prototype.

# LISTING 10.12 KILOS.H

```
//==================================================
// kilos.h -- Function kilos() header file
// Copyright (c) 1999 by Tom Swan. All rights reserved.
//==================================================

// Function prototype
double kilos( double miles );
```

In practice, most header files declare several function prototypes along with other items such as constants. They might also declare global variables. But, in this case, the kilos.h header file merely declares a prototype for the kilos() function. Listing 10.13, kilos.cpp, implements the function.

# LISTING 10.13 KILOS.CPP

```
//==================================================
// kilos.cpp -- Function kilos() implementation module
// Copyright (c) 1999 by Tom Swan. All rights reserved.
//==================================================

// Convert miles to kilometers
double kilos( double miles )
{
    return miles * 1.609344;
}
```