method assumes the context to be complete and stable. While in the constructor, the compiler considers the context to be incomplete or unstable.

Static methods of a class do not depend on a context, so you can use them basically anytime and anywhere. In fact, you don't even need an instantiated object to use them. So, the relationship between the static methods and class is very loose, almost ancillary. Classes rarely use static methods because of this loose relationship. However, they are useful on certain occasions. Some system calls, such as signal handlers, do not support the contexts that standard methods require. So if, for example, you want to capture various signals in a class, you must declare the signal handlers as static methods.

# Destructors: What Requires Cleanup

Just as constructors initialize the object and get it ready for use, destructors reverse some of the steps and get the object ready for the free heap. Unlike Java, which uses a garbage collector to free up space, C++ requires you to manually clean up objects.

Often, the objects are self-contained and require little more than freeing the space. However, some classes (such as SimpleString and TextMessage) use some of the heap. The compiler cannot tell if the pointers in these classes really point to anything more than one element. Destructors let you specify what needs to be cleaned up and when.

Other typical cleanup steps include closing files and unhooking handlers. The following is the destructor for the Socket class:

```
```
//********************************************************
//*** Socket destructor
Socket::~Socket(void)
{
   if ( close(SD) != 0 )
      throw FileException("Can't close socket");
}
```
```

You should declare all destructors as virtual so that all destructors in the inheritance hierarchy get executed. A non-virtual destructor indicates that you do not want the parents' destructors to fire when you delete an object. You can just specify the superclass's destructor as virtual—this makes all inherited destructors virtual as well. However, for clarity, you may want to explicitly declare them as virtual.

# Testing the Socket Framework

The Socket Framework is a custom implementation based on the criteria that the previous sections described. The following sections show you how to use it by stepping you through a couple of examples. The Web site that accompanies this text has a few other examples that show you how to implement datagram, broadcast, and multicast sockets.

# The Echo Client/Server

The first example (and the most cited throughout the text) is the echo client/server. The real reason for using an echo client/server is to test that the communications work correctly. After you have that part down, the rest is easy.