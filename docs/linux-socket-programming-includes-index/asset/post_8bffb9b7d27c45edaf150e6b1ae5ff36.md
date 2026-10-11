
calling the `start()` method creates a new execution thread and starts the task at your custom implementation of `run()`. Synchronizing a multithreaded class is fairly easy with two tools: synchronized methods and execution yielding.

Analyzing and using Java as a programming base helps you to see how you can deploy sockets in an object-enabled language. The next chapter proposes and lays out an implementation in C++.

## 12

## Using Java’s Networking API

## Designing and Using a C++ Socket Framework

## CHAPTER 13

### IN THIS CHAPTER

- Why Use C++ for Sockets Programming? 284
- Laying Out the Framework 286
- Testing the Socket Framework 296
- Implementation Limitations 299
- Summary: A C++ Socket Framework Simplifies Programming 301

The last chapter showed you how to program sockets in Java. Java is a very powerful language and has many advantages, such as platform independence, JIT (Just In Time) compiling, and even native compilers/converters. However, not everyone wants to use Java, claiming lack of stability or needed performance, and some may be more inclined to use a C++ version instead. Writing a socket *framework* (or class library) takes in all technologies described in this book. In fact, this chapter offers a few additional socket features that are covered in Part IV, “Advanced Sockets—Adding Value.”

To use this chapter, you must be familiar with C++ and object programming. As in earlier chapters, it is assumed that you know how to write in C++ and compile and link the files. Tutorials for these procedures are easy to find on the Internet.

This chapter steps you through the process of analyzing, designing, and creating a class framework. This particular framework only provides a wrapper (an interface with little added functionality) around the Socket API. You can still use these principles to define other frameworks, not just wrappers.

## Why Use C++ for Sockets Programming?

A C++ framework that wraps the Socket API offers several advantages over making the individual system calls manually. As you may have noticed, the process of creating, configuring, and using a socket varies very little from application type to application type.

### Simplifying Sockets Interfacing

Writing a class that matches the application type lets you focus more on the programming and less on the network. The sockets interfacing is not difficult but requires specific steps to get the communication channels to work consistently.

The C++ language is more powerful than C, and is a complete superset of C’s feature set. In fact, you can compile C++ programs with the same tool as with C (*cc*). (In reality this is not 100% accurate. When *cc* discovers a .c or .cpp extension, it calls *g++* instead of *gcc*.) Along with this additional power, the C++ language is quite a bit more complicated as well. Nevertheless, the advantages outweigh the drawbacks.

Writing a Sockets Framework lets you define simpler interfaces for others to use. Program simplicity is imperative for testability and defect fixing. Additionally, the simpler the interface, the easier it is to use. Similarly, the easier something is to use, the more likely it is used correctly and frequently.

A properly designed and written C++ framework offers very easy and direct interfaces that let the programmer really focus on the job at hand.

## Hiding Implementation Details

Interfaces promote the simplicity or complexity of a product. As the interface’s complexity increases, the ease of use diminishes. Hiding implementation details is very important for ensuring simplicity. The design and implementation—particularly in a wrapper—attempt to hide details from the user-programmer.

Of course, the user-programmer may want to know how you did certain things, but that information can hurt you and him or her. Encapsulation, one of the foundations of objects identified in Chapter 11, “Saving Time with Objects,” protects both the framework writer and the user-programmer. By hiding how you implement certain steps, you protect the programmer from changes in those implementations. This also protects the framework by allowing the system to evolve internally without affecting the interfaces to the outside world.

As with all other object-enabled languages, C++ enforces the rules of ownership so that the program can only access what it can see and own. If planned well, one framework can support all forms of socket networks.

## Deploying Reusable Components with Easy to Use Interfaces

Interfaces and hiding implementation details creates a very thin membrane between the program and the framework. The program must pass all requests through this membrane. The operations inside the class accept and work on the data and requests.

Keeping the interfaces simple is very important. The result is clear: a set of program tools that many programs can use. In fact, several implementations can exist for the same interface. You simply choose the one that behaves the best for the circumstances.

As you write these tools, the clear advantage of reuse becomes apparent to the user-programmers. They in turn promote your work by releasing programs based on these tools. (An excellent example is QL.)

## Demonstrating the Framework Design Processes

Framework tools exist on the Internet. You can find various flavors’ forms. Finding a sockets framework, on the other hand, is a little more difficult. Writing one here lets you configure it in whatever form you would like and has an added bonus of showing the process of writing tools.

Unlike the UML-style of OOA/D, writing libraries or frameworks works more from the bottom than entirely from the top. OOA/D states that you must start with the requirements and eventually build a product—similar to peeling an onion. The whole idea is to minimize feature-creep and implement only what is needed.

![](img/2591af4bdf00a0f382331fc9481f785e_304_0.png)

Framework creation takes a different perspective: the features that the user-programmer desires are not yet known, so the framework implements as many features as the user-programmer might use. This approach, of course, just shouts: “We want features” which can raise a concern of dead code (linked-in unused/unbearable code). Dead code does not occur much in programs anymore. Newer, smarter linkers excise all code that appears to be unneeded.

## Laying Out the Framework

Creating an object framework is similar to framing a wall: You begin with set dimensions and nail everything together in a specific order. This section lays out the steps for creating a framework by identifying the features, grouping into components, organizing the hierarchy, and so on.

### Defining the General Features

The framework must depend on some kind of related requirements. A program that has too few requirements is uninteresting (and not worth implementing), and a program that has too disparate requirements yields an awkward result. The requirements define the parameters in which the framework must operate.

Often, when you get a list of wanna-haves, the list is not detailed enough for analysis. Be prepared to ask questions. The sockets framework must support most of the major capabilities described in this book.

### Supporting the Different Types of Sockets

The primary feature of an Internet sockets framework is access to the protocols. The first protocol that this book mentions is a TCP connection. This style of programming always has a client and a server. The server awaits a client’s request for a connection, creates a distinct connection to it, and then interacts with the client.

Another communication capability connects one host to another as peers. This style does not really have a client or server exactly, but it does have an initiator and a replier. Also, it uses a UDP connection.

Two additional types of communications are broadcasting and multicasting, discussed later in the book. Both allow you to send messages to several destinations at the same time. For more information on these protocols, please refer to Chapter 15, “Network Encapsulation with Remote Procedure Calls (RPCs).”

The last two types of sockets are far too low-level for this framework: raw and promiscuous sockets. These types could be integrated in this framework but, because of the level of detail and management required, these are best left to direct API use. Feel free to revise the framework to include these features as you desire.
