# USING VARIABLE DATA TYPES

When you assign a type to a variable in VB.NET, you essentially specify what particular kind of data a variable can store. For example, you may need to store a number to use in your program. To do so you create a variable capable of storing the number. If you store text later, you cannot use the same variable. You must declare a variable that stores text.

Variable types cannot change as a program runs. If you store a number into a Short variable type, you cannot use the variable to store other types of data, such as an Integer. When you assign data of a different type to a variable, VB.NET converts the data if possible and assigns the converted value to the variable.

Ten different basic variable types allow the storage of a variety of data. Many of the types, such as Short, Integer, and Long, represent the same type of data, only in different sizes. For example, Short can only store a whole number value from -32768 to 32767. An Integer expands that range to about -2 billion to 2 billion. Long extends that range to +/- 9 quintillion (9 x 10^18).

Programmers call the process of converting variables from type to type casting. Casting is done automatically when necessary in VB.NET, unless you have defined Option Strict as True in the project preferences. Casting can cause loss of information. For example, if you convert a Single, which stores decimal point numbers, such as 12.24, into a Short, VB.NET chops the value to 12 because a Short lacks the ability to work with decimals.

Using the largest available variable can adversely affect how fast your program runs. Use a variable size, therefore, that holds your data but is no larger than necessary.

# USING VARIABLE DATA TYPES

![](bbox=[0.03, 0.57, 0.98, 0.82])

+   1. Create a new project or open an existing one.
+   2. Open the method in which you want to declare a variable.
+   3. Type Dim MyBoolean to declare a variable, replacing MyBoolean with the variable name you want to create.
+   4. Type As Boolean, replacing Boolean with the variable type you want to create.
+   The IntelliSense window appears. You can type the appropriate code or click the entry in the list.
+   You can assign a value by typing an equal sign and the appropriate value.