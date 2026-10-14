+   - Check the results of all expressions using a hand calculator. Keep in mind, however, that the internal binary formats in your system and calculator might differ, as might the algorithms used to display rounded values, so don't expect the results to be exactly the same. For example, my calculator shows 75.5 degrees Fahrenheit equal to 24.166666 degrees Celsius. The celsius.cpp program reports a rounded value of 24.1667.
+   - Don't use floating point variables in accounting software to store monetary amounts. Use the long or long long values and assume two decimal places in the values. (In other words, store monetary values in cents and the lowest practical denomination in your currency.) Chapter 8, "Controlling Input and Output," in the section "Lucky Pennies" lists a sample program, money.cpp, that shows one way to use long and long long values this way.
+   - When calling functions—especially those that operate on C-style strings—be sure that you don't mix up the order of any arguments. The statement strcpy(A, B) does not copy A to B, as might seem intuitively correct. It copies string B to A. Check the online info and man-page documentation for standard functions, especially the first time you use one.

# SUMMARY

GNU C++ provides seven numeric data types: char, short, int, long, float, double, and long double. An eighth type, long long, can store truly huge integer values but is probably unique to GNU C++. This chapter introduced numeric data types and also explained how to use C-style strings, composed of one or more characters and ending with a terminating null. The chapter also showed how to create arrays and structures, and explained GNU debugging commands to investigate a program's data.

For more information on subjects introduced in this chapter, turn to the following chapters:

+   - Chapter 5, "Compiling and Debugging C++ Programs"
+   - Chapter 8, "Controlling Input and Output"
+   - Chapter 9, "Controlling Program Flow"
+   - Chapter 10, "Creating and Calling Functions"
+   - Chapter 11, "Managing Memory with Pointers"