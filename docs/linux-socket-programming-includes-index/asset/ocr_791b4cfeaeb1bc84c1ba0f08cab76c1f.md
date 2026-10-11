Constructors differ very slightly from regular methods; you can do most operations as you would in a regular method—create objects, allocate space, perform calculations, and so on. For example, the following is the declaration of the Socket class constructor:

```
```c++
//************************************************************
//*** Default Socket constructor
//*** Using the Network (PF_INET) and Protocol (SOCK_STREAM),
//*** create a socket and place the reference in the SD
//*** attribute.
Socket::Socket(Elnetwork Network, Eprotocol Protocol)
{
    SD = socket(Network, Protocol, 0);
    if ( SD < 0 )
        throw NetException("Could not create socket");
}
```
```

If anything goes wrong in the creation, you do not have a way of sending back an error with conventional methods. Instead, the framework uses exceptions to send the error directly to the handler. If everything goes well, the construction finishes and returns to the caller.

Not all operations are available to a constructor. You cannot call methods to the class you are creating unless they are declared static. Each class carries with it a context or its state. Every method assumes the context to be complete and stable. While in the constructor, the compiler considers the context to be incomplete or unstable.

Static methods of a class do not depend on a context, so you can use them basically anytime and anywhere. In fact, you don't even need an instantiated object to use them. So, the relationship between the static methods and class is very loose, almost ancillary. Classes rarely use static methods because of this loose relationship. However, they are useful on certain occasions. Some system calls, such as signal handlers, do not support the contexts that standard methods require. So if, for example, you want to capture various signals in a class, you must declare the signal handlers as static methods.

# ### Destructors: What Requires Cleanup

Just as constructors initialize the object and get it ready for use, destructors reverse some of the steps and get the object ready for the free heap. Unlike Java, which uses a garbage collector to free up space, C++ requires you to manually clean up objects.

Often, the objects are self-contained and require little more than freeing the space. However, some classes (such as `SimpleString` and `TextMessage`) use some of the heap. The compiler cannot tell if the pointers in these classes really point to anything more than one element. Destructors let you specify what needs to be cleaned up and when.