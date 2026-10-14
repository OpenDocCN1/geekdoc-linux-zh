
## Summary

A typical program contains many functions, each with a specific purpose. Functions modularize a program and make it easier to write and maintain. Functions can declare value, reference, and pointer parameters to which statements pass arguments. Functions may also return values of any valid C++ type. Before using a function, a program must declare it using a prototype that states the function's return type, its name, and any parameters. In addition to introducing functions, this chapter also explained recursive functions and how to use C++ features such as default argument values, inline functions, and overloaded functions. The chapter ended with a look at debugging commands useful for tracing function statements and examining parameter values.

For more information on subjects introduced in this chapter, turn to the following chapters:

- Chapter 5, “Compiling and Debugging C++ Programs”
- Chapter 6, “Creating Data Objects”
- Chapter 11, “Managing Memory with Pointers”
- Chapter 23, “Using the Standard Template Library (STL)”

## Chapter 11: Managing Memory with Pointers

Modern software can use a bumper crop of memory, and programmers need reliable techniques for managing this space. In this chapter, you learn how to use C++ memory-management techniques to create dynamic objects such as large buffers for holding file data and arrays that expand and contract at runtime. These methods help your programs take advantage of the tremendous amount of memory available on modern PCs and also prepare you for Part III, "Object-Oriented Programming," in which memory management plays an even bigger role in software development.

### Allocating Memory

Generally, to create an object in memory, you request space from the GNU C++ memory manager. It isn't necessary to know beforehand exactly where the memory exists or its organization. If enough memory is available, the memory manager reserves space for the object and gives you its address. The program uses that address as a pointer to the dynamic object's value. The object can be a simple variable, but it is more commonly a complex type such as struct, a string, or an array.

There are two basic ways to create dynamic objects. You can call standard C library functions such as malloc() (memory allocate) and free(). Or, you can use the C++ operators new and delete. I show both methods in the next sections. You need to know how the standard C functions work, if only to understand their use in existing programs. However, in new code, you should use the C++ operators. They are safer and easier to use correctly, and they play a major role in the rest of this book's focus on object-oriented C++ programming.

### Memory Management with new and delete

C++ adds two operators to the C language, new and delete. These are not functions. They are native operators. Use new to allocate space for a dynamic variable. Use delete to free that space after the program is finished using it. Freeing memory returns it to the memory pool, sometimes called the heap. This makes the space available for use in creating other dynamic variables.

Although most dynamic objects are complex types such as structs and arrays, you may use new to allocate memory for an object of any data type. For illustration, it's useful to run through some examples using a simple type such as double. For example, the following statement uses the new operator to reserve space for a dynamic double object. It is called "dynamic" because the object comes and goes under the control of the program:

```cpp
double *dp = new double;
```

That statement actually performs three distinct actions:

- It declares a pointer named dp to a double object.
- It uses new to allocate enough memory to hold one double object.
- It assigns to dp the address of the allocated memory.

Following the statement, dp points to a double object in memory. Stored in dp is the address of the first byte of that memory. Like an arrow pointing to an office in a building, a C++ pointer refers, or points, to an object in memory.

You don’t have to declare and initialize a pointer in one step. You can declare the pointer ahead of time, and then elsewhere use new to allocate memory and assign its address to the pointer. This is a common technique for creating a dynamic object, demonstrated by this code fragment:

```cpp
double *dp;    // Declare a pointer to a double object
...           // dp is uninitialized here!
dp = new double;  // Allocate space for a double object
```

Merely declaring the pointer in the first statement does not allocate memory for a double object. That takes place later in the statement that uses new. Until that second statement executes, the pointer dp is uninitialized, analogous to an arrow in an unfinished building that points to a room not yet constructed. Following the arrow to its nonexistent destination could be hazardous to your health. Similarly, using an uninitialized pointer before it is allocated memory is nearly guaranteed to cause a serious bug.

> **Tip**
> The phrase "a pointer to a double object" is commonly shortened to "a pointer to double" or "a double pointer."

The new operator reserves exactly enough space in memory to hold one object of the specified type—in this case, 8 bytes, the size of one double variable. Some additional space might be attached to the allocated memory for the memory manager's internal use, and for efficiency reasons, memory might be allocated in certain block sizes. However, as far as the program is concerned, exactly eight bytes are available for holding one double, floating-point value. The exact location of those bytes is usually unimportant. The pointer dp always locates the allocated memory, wherever it happens to be.

> **Note**
> If enough memory is not available, new throws an exception, which if not handled ends the program. Chapter 16, "Handling Exceptions," explains how to trap this exception and deal with such errors. Also see "Dealing with Memory Errors" later in this chapter.

After allocating memory to a pointer such as dp, you can store a value of its declared type in that memory, and then use it as you can any other variable of that type. However, dp alone is not a double object. It is a pointer to a double object. To use dp as a double object requires dereferencing the pointer with the * operator. This statement, for example, assigns a value to the double object to which dp points:

```cpp
*dp = 3.14159;
```

That copies the value 3.14159 into the location in memory addressed by dp. You might think of the dereference operator, *, as a conduit that creates a channel to the addressed
