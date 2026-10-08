your source code in some way. For example, the #include directive causes the pre-processor to include another file in your program, at the point where the #include directive appears.

The file **stdio.h** is called a **header file** and is part of your C development system. This file contains information the compiler needs to process standard input or output statements. Any program that performs standard input or output must include the stdio header file. Because the sample program uses the printf statement (which performs standard output), it must include stdio.h.

The C development system includes a number of header files. All library functions require that you include a particular header file.

# ### Specifying Data Types

Variables and constants represent data used in a C program. You must declare variables and state the type of data that the variable will hold. A variable's data type determines the upper and lower limits of its range of values. Data types with wider ranges of values occupy more memory than those with narrower ranges. The exact limits of the ranges vary among compilers and hardware platforms.

Table 10-2 shows a list of the basic data types that may be used in a C program.

| Data Type | Description |
| :--- | :--- |
| char | Occupies a single byte. Designed to hold one character from the character set used by the running machine. |
| int | Holds integer values. The size of an int variable should be the default size of an integer on the running machine, but it is not always. |
| float | A single-precision, floating-point value. |
| double | A double-precision, floating-point value. |

**Table 10-2:** C data types

As mentioned earlier, the exact upper and lower limits of each of the range of values for data types depends on the compiler and hardware platform being used. You can use three modifiers with int data types: short, long, and unsigned. The short and long modifiers make an integer variable smaller or larger than its default size. Typically, a long int occupies twice as many bits as an int. On some machines a short int occupies half the number of bits as an int, but in many cases there is no difference between a short int and an int.