However, C++ is much more strict about enforcing type compatibility among objects used in assignment statements. To tell the compiler that you intend to convert malloc()’s return value of type void * into a double *, you must preface the call to malloc() with the type cast expression (double *). When converting C programs to C++, this is one change you might have to make. (It is preferable, although possibly more time-consuming, to convert all uses of malloc() to use the new operator.)

To malloc(), pass the size in bytes of the amount of space to reserve. Usually, the safest course is to use sizeof() along with the data type of the object. Even so, you might spot an inherent danger here. A simple typing error such as the following allocates an incorrect amount of space:

```
dp = (double *) malloc( sizeof(char) ); // ???
```

Oops. The program just reserved a single byte (the size of a char object) and assigned its address to dp. Even with all warning levels engaged, the compiler is happy to enable you to make this grave error, one more good reason to use the C++ new operator, which obtains the size of an object from its data type. In C++, an obviously incorrect statement such as this

```
double *dp = new char; // ???
```

results in the following compiler error:

```
test.cpp:9: assignment to ‘double *’ from ‘char *’
```

Getting back to C, if malloc() returns a non-NULL pointer, you may use it in the same way as described in the preceding section. When you are finished using the dynamic object, delete that memory by calling free():

```
free(dp);
```

That returns the allocated memory to the heap for use in creating other dynamic objects. If dp is NULL, deleting it does no harm, so it is not necessary to include a test for a NULL pointer before calling free(). The same comments from the preceding sections about deleting pointers apply to standard C memory management. Always free the memory your program allocates.

> Warning
> You may combine C and C++ memory techniques in the same program. However, if you allocate space using malloc() or another standard C library function, always use free() to delete that space. If you allocate space using new, always use delete. Although you might discover in the GNU source files that new calls malloc(), it is not safe to assume that the two methods are equivalent! As you learn in Chapter 19, “Overloading Operators,” a C++ program can reprogram the new operator to use an entirely different memory management system. In such cases, mixing C and C++ memory techniques is begging for disaster. Don’t do it.