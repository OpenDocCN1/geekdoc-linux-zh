So far, so good. The statements construct two TPrompt objects, tp1 and tp2, and prompt the user to enter two strings. But think about what happens if the program copies one of those objects to the other:

```
tp1 = tp2; // ???
```

That may look innocent enough—it is perfectly acceptable to the compiler—but the assignment causes the tp_string pointer in tp2 to be copied to the tp_string pointer in tp1. Now both pointers address the same memory, causing not one but two bugs. The original tp_string pointer in tp1 is overwritten—its addressed memory is lost in space. Worse, because both pointers now address the same dynamic memory, when the two objects go out of scope, the ~TPrompt() destructor attempts to delete the identical dynamic memory block twice. That leads to a dreaded "segmentation error" by attempting to access memory the program doesn't own, and the process ends abruptly with—you guessed it—a core dump.

To prevent this kind of problem, as a general rule, any objects that own dynamic memory need to provide programming to handle the copying of one object to another. There are two times that this can occur:

+   - When a new object is constructed using another object
+   - When one object is assigned to another

To handle these situations, the class needs two new functions. The copy constructor creates a new object using the value of another existing object of the same class. (They may also be of related classes, as Chapter 14, "Investing in Inheritance," explains.) The second needed function, named operator=(), handles assignments of one existing object to another that has already been constructed. Both functions use similar code. In general, a copy constructor has the following form:

```
TAnyClass(const TAnyClass &copy);
```

Like all constructors, the copy constructor is named the same as its class, and it has no return value. Its single parameter is a const reference to an object of the same class. C++ calls the copy constructor for objects created using statements such as the second two here:

```
TAnyClass t1;      // Calls default constructor for t1
TAnyClass t2 = t1;  // Calls copy constructor for t2
TAnyClass t3(t2);   // Calls copy constructor for t3
```