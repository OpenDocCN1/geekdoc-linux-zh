# USING POINTERS IN CLASSES

Using pointers to address dynamic class objects is only half the story of classes and dynamic memory. A class object may also own other dynamic objects of classes with their own rules of creation and destruction. To illustrate, consider the following hypothetical class, declared and implemented entirely inline:

```
class TAnyClass {
private:
    TDate *tdp;
public:
    TAnyClass() { tdp = new TDate(1, 1, 2000); }
    ~TAnyClass() { delete tdp; }
};
```

The class declares a private pointer, tdp, to a TDate object. Because tdp is private, only statements in the class's member functions may refer to tdp. The object that tdp addresses is created when the TAnyClass object is constructed, a task handled in this case by the TAnyClass() constructor. The constructor's inline statement uses new to construct a TDate object and assign it to the private tdp pointer.

The class destructor deletes the memory that the constructor allocates, and in this way, the memory allocated to tdp is neatly managed. When the program constructs a TAnyClass object, the constructor allocates memory for a TDate object addressed by tdp. When the TAnyClass object goes out of scope or is deleted, the destructor deletes the TDate object addressed by tdp. The class carries out its memory management responsibilities so that the users of the class don't have to attend to these details.

> Note
> You may question whether the delete statement shown here might mistakenly delete an uninitialized tdp pointer. However, that can't happen because, if new cannot fulfill the request for memory, it throws an exception and the TAnyClass object is not constructed. (In general, exceptions thrown in a constructor result in the object not being constructed.) Consequently, because the object is not constructed, its destructor is never called, so even if the use of new fails here, there is no danger of deleting an uninitialized pointer. See Chapter 16, "Handling Exceptions," for details on this topic.

# CLASS MEMORY MANAGEMENT

Listing 13.2, prompt.cpp, puts the preceding concepts to work and shows how to manage dynamic memory owned by a class object. The program declares a class that encapsulates the get_string() function from Chapter 11, "Managing Memory with Pointers." The result is a class that you can use to create an object for prompting and storing a line of text entered by the program's user. By encapsulating this code in a class, the constructor and destructor automate memory allocations, whereas in the original code, memory management is the user's responsibility.