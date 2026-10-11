The last chapter showed you how to program sockets in Java. Java is a very powerful language and has many advantages, such as platform independence, JIT (Just In Time) compiling, and even native compilers/converters. However, not everyone wants to use Java, claiming lack of stability or needed performance, and some may be more inclined to use a C++ version instead. Writing a socket *framework* (or class library) takes in all technologies described in this book. In fact, this chapter offers a few additional socket features that are covered in Part IV, “Advanced Sockets—Adding Value.”

To use this chapter, you must be familiar with C++ and object programming. As in earlier chapters, it is assumed that you know how to write in C++ and compile and link the files. Tutorials for these procedures are easy to find on the Internet.

This chapter steps you through the process of analyzing, designing, and creating a class framework. This particular framework only provides a wrapper (an interface with little added functionality) around the Socket API. You can still use these principles to define other frameworks, not just wrappers.

# Why Use C++ for Sockets Programming?

A C++ framework that wrappers the Socket API offers several advantages over making the individual system calls manually. As you may have noticed, the process of creating, configuring, and using a socket varies very little from application type to application type.

# Simplifying Sockets Interfacing

Writing a class that matches the application type lets you focus more on the programming and less on the network. The sockets interfacing is not difficult but requires specific steps to get the communication channels to work consistently.

The C++ language is more powerful than C, and is a complete superset of C’s feature set. In fact, you can compile C++ programs with the same tool as with C (*cc*). (In reality this is not 100% accurate. When *cc* discovers a .c or .cpp extension, it calls *g++* instead of *gcc*.) Along with this additional power, the C++ language is quite a bit more complicated as well. Nevertheless, the advantages outweigh the drawbacks.

Writing a Sockets Framework lets you define simpler interfaces for others to use. Program simplicity is imperative for testability and defect fixing. Additionally, the simpler the interface, the easier it is to use. Similarly, the easier something is to use, the more likely it is used correctly and frequently.

A properly designed and written C++ framework offers very easy and direct interfaces that let the programmer really focus on the job at hand.