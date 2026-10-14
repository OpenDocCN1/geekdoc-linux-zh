
properly deleted when an object such as prompt1 goes out of scope or is deleted, C++ calls the class destructor for that object. Take a look at the destructor's programming:

```
TPrompt::~TPrompt()
{
    cout << "Entering destructor for string "
         << tp_string << endl;
    delete[] tp_string;
}
```

As with constructors and member functions, the destructor's header specifies the class name (TPrompt), the C++ scope resolution operator (::), and the function's name, ~TPrompt(). Unlike constructors and member functions, destructors may not declare any parameters. A destructor also has no return value. You may implement destructors inline directly in the class declaration, or you can implement a destructor as shown here independently of its prototype in the class.

> Tip
> A class may have one and only one destructor. If you need to have different ways to destroy class objects, use flags or values that the destructor's code can inspect and take action accordingly.

For illustration, the ~TPrompt() destructor displays a message so that you can trace when it is called in the sample program, but the second statement is all that's needed. It deletes the memory allocated to tp_string. Because the class destructor is called automatically when a TPrompt object goes out of scope, the destructor ensures that the allocated memory is also deleted. If you haven't done so already, compile and run the program, and observe when the destructor is called for the program's two sample input prompts. Here's a sample run:

```
$ g++ prompt.cpp
$ ./a.out
Prompt #1: aaaa
You entered aaaa
Prompt #2: bbbb
You entered bbbb
Entering destructor for string aaaa
Entering destructor for string bbbb
```

To the first prompt, I typed aaaa. To the second, I typed bbbb. In both cases, the object's destructors are called to delete the memory allocated to the input strings. The last two lines show that, in both cases, the ~TPrompt() destructor cleans up the objects before they are themselves destroyed.

## COPY CONSTRUCTORS

The preceding version of the TPrompt class is not entirely safe for use. To understand why, consider what happens if you create two dynamic TPrompt objects tp1 and tp2 using the following statements (refer back to Listing 13.2, prompt.cpp):

```
TPrompt tp1("Enter first string: ");
TPrompt tp2("Enter second string: ");
```

So far, so good. The statements construct two TPrompt objects, tp1 and tp2, and prompt the user to enter two strings. But think about what happens if the program copies one of those objects to the other:

```
tp1 = tp2; // ???
```

That may look innocent enough—it is perfectly acceptable to the compiler—but the assignment causes the tp_string pointer in tp2 to be copied to the tp_string pointer in tp1. Now both pointers address the same memory, causing not one but two bugs. The original tp_string pointer in tp1 is overwritten—its addressed memory is lost in space. Worse, because both pointers now address the same dynamic memory, when the two objects go out of scope, the ~TPrompt() destructor attempts to delete the identical dynamic memory block twice. That leads to a dreaded "segmentation error" by attempting to access memory the program doesn't own, and the process ends abruptly with—you guessed it—a core dump.

To prevent this kind of problem, as a general rule, any objects that own dynamic memory need to provide programming to handle the copying of one object to another. There are two times that this can occur:

- When a new object is constructed using another object
- When one object is assigned to another

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
