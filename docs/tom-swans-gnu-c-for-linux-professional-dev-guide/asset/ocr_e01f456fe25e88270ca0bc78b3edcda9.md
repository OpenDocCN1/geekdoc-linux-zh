The preceding chapter introduced the class and showed several ways to construct class objects. However, the simple classes you have seen so far are not of much practical use. In the real world of programming, classes need more sophisticated devices for safely allocating and destroying dynamic memory, and for passing objects efficiently to and from functions.

This chapter introduces those topics, and ends with a version of the Date class that encapsulates some of the functions and data types of the standard library’s date and time routines. Along the way, the chapter explains techniques for using a destructor to clean up objects when they are destroyed, for managing dynamic memory using copy constructors, and for using something called the operator=() member function to copy one object to another. Finally, the chapter ends with a discussion of declaring and implementing classes in separate modules.

# DESTROYING CLASS OBJECTS

As the preceding chapter explained, class constructors initialize newly created class objects. On the flipside of that coin, it is also frequently necessary to destroy objects in a controlled manner. For example, when an object owns a pointer that addresses dynamic memory, the program must delete that memory when the object itself is destroyed. To perform that and other cleanup duties, a class declares a destructor.

# INTRODUCING THE DESTRUCTOR

Like a constructor, a destructor has the same name as its class but is preceded with the character ~, used in scientific circles and sometimes in programming as a negation symbol. A destructor is, in a sense, the negation of a constructor—what a constructor builds, a destructor destroys. To illustrate destructors, the following code fragment declares a bare-bones class with constructor and destructor prototypes:

```
class TAnyClass {
public:
    TAnyClass();    // Constructor
    ~TAnyClass();   // Destructor
};
```

If the program declares a TAnyClass object, as in the following statement, the class constructor is called to initialize that object:

```
TAnyClass an_object;   // Calls the TAnyClass() constructor
```

When an_object goes out of scope—for example, when its declaring function returns—the object is destroyed. At that time, C++ automatically calls the ~TAnyClass() destructor to give the object the opportunity to perform any cleanup chores before it is tossed away for good. C++ calls the destructor also if the program creates a dynamic TAnyClass object with new operator and then deletes the object:

```
TAnyClass *tp = new TAnyClass;   // Calls TAnyClass() ctor
// ... statements that use the object
delete tp;                     // Calls the ~TAnyClass() dtor
```