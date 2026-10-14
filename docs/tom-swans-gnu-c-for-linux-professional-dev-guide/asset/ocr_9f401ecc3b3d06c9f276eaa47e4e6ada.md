# CREATING A CONTAINER CLASS

A classic and most useful application for virtual functions is the development of container classes. A container is a general purpose object that can store other objects. To use a container, you simply construct an object of a container class and stuff your data objects into it. A well-designed container can store, search, sort, and perform other jobs on objects. Because they are designed using C++ object-oriented classes, containers tend to be far more versatile, and much safer, than other common C and C++ storage mechanisms such as arrays and linked lists.

In the coming sections, you develop the TContainer class, which can store and sort data objects. The class is usable, but to keep it within a reasonable size for listing in this book, it is stripped of miscellaneous functions. However, in describing the programming, I suggest some modifications for creating a practical container class based on TContainer.

> Tip
> You may declare pointers and references to abstract classes such as TShape, but because you cannot create abstract class objects, it isn’t possible to pass TShape objects by value to function parameters.

> Note
> The TContainer class listings are more lengthy than most in this book. To make the programming more comprehensible, I divided the listings into pieces. The full text is in files container.h, container.cpp, and tcontain.cpp on the CD-ROM.

# ABSTRACT CLASSES

Listing 15.1, container.h, shows about half of the container.h header file. This part of the header file declares the TObject abstract class as the basis for data objects to be stored in a container.

# LISTING 15.1 CONTAINER.H (PARTIAL)

```
#define DEFAULT_SIZE 100     // Default container capacity

class TObject;               // Incomplete class declaration
typedef TObject * PTObject;   // Pointer to a TObject object
typedef PTObject * PPTObject; // Pointer to a TObject pointer

// Abstract class for items to store in a container
class TObject {
public:
    virtual ~TObject() {};
    virtual int Compare(PTObject p) = 0;
    virtual void Display() = 0;
};
```