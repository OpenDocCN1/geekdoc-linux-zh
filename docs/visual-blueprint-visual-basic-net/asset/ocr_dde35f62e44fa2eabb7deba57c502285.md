# CREATE A SHARED VARIABLE

A global variable is a variable that any part of your application can access, meaning all parts of your application access a single instance of created data when the program initializes. In many programming languages, such as Visual Basic 6 and C++, you declare global variables outside of all class modules to alert the language to declare the variable globally. VB .NET provides an improved version of global variables called shared variables, which you place inside a class, but which still allow you to access a single instance of data throughout your application. Declaring shared variables inside of classes allows you to create more readable code that maintains the modularity of classes with the flexibility of globally available data.

You declare a shared variable inside a class much like a standard member variable. Unlike a standard member variable, the application can access the shared variable without creating an instance of the class. Also, even if no instances of the class exist, the variable remains in memory and never loses its value. For example, say your program has a counter class. Normally, you create an instance of the counter class and make sure not to lose the reference to it throughout your program's operation. Using a shared variable, you can instantiate the class when necessary to update the counter, but the shared member variable keeps the value of the counter at all times.

You create a shared member variable by placing the Shared keyword before the variable name, but after the Dim or accessibility keyword. When you declare a shared variable Public, you can read or modify the variable from any module that has access to the class. To access the shared variable outside of the class, you use the name of the class, following it with a period and the name of the variable. You can also access the variable normally using an instance of the class. To access members of a class, see Chapter 5.

As with standard private member variables, you cannot access shared member variables you declare Private outside of the class. The variable stores value in memory across instances of the class. The value does not reset when you create a new instance of the class. This means if one instance of the class changes the variable, all other instances of the class work with the same new value. See Chapter 5 to learn more about member accessibility.

# CREATE A SHARED VARIABLE

![](bbox=[0.06, 0.68, 0.94, 0.88])

+   1. Create a new class or open an existing one.
+   2. Type an accessibility keyword such as Public or Private on an empty line inside the class outside of methods and events.
+   3. Type Public Shared Property1 As String, replacing Public with the proper accessibility, Property1 with the variable name, and String with the variable type.
+   You can repeat steps 2 and 3 as necessary.