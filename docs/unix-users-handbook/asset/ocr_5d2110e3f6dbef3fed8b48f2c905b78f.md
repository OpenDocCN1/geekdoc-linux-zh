# ## Reference Data Types

Non-primitive data types in Java are objects and arrays and are often called “reference types”. These types are handled by reference, meaning the address of the object or array is stored in a variable and passed to methods.

In C, value by reference can be manipulated using the & operator and dereferenced using the * and -> operators. These operators do not exist in Java.

# ## Modifiers

Modifiers may be applied to variable and/or method declarations to provide additional information or to place restrictions. Java defines a number of modifier keywords.

The final keyword can be applied to classes, methods and variables. A final class may never be a subclass. A final method may never be overwritten. A final variable may never have its value set.

The native keyword is a modifier that may applied to method declarations, indicating that the method is implemented elsewhere in C or another platform dependent implementation.

The synchronized keyword prevents concurrent modification of the class does not occur, indicating that the class is not thread-safe.

The transient keyword can be applied to instance fields within a class, indicating that the field is not part of an object’s persistent state and does not need to be serialized with the object.

The volatile keyword indicates that synchronized threads are using a field, and the compiler should not attempt to perform optimizations with it. For example, it may indicate that the value of the variable should be read from memory every time and should not have a copy saved on the stack.