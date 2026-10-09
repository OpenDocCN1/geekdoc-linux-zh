Typically, these components are heterogeneous objects contained in a single interface. Some object analysts call these groups *packages*, due to the method of distribution, or *patterns*, and because the systems of objects often fit in generalized ways. But, they can also be hierarchies with abstract objects as the primary interface.

This section describes the four basic components of the Socket Framework. Each of these components as a hierarchy as previously described.

# Exceptions: Handling Problems

All frameworks should identify and use exceptions. The kinds of exceptions you may want to capture include networking, I/O, boundary, and so on. The exception hierarchy depends on the *Exception* class for basic functionality. **Figure 13.1** displays the exception component.

> **Figure 13.1. All exception classes derive from *Exception*, which captures only a string and the error code.**

![](bbox=[0.18, 0.33, 0.83, 0.62])

An exception class hierarchy infrequently defines any startling or ingenious design. In fact, if you employ a class hierarchy for exceptions, be very careful that you do not create a potential for recursive exceptions. For example, if you allocate memory and have mapped the memory handler to an exception, you could crash the program from one bad *new()* call. Leave the design of exceptions to the simplest form with little more than values and a brief message.

# Messages: Packaging and Shipping the Data

To send and receive messages through the I/O subsystem, you need blocks of data and buffers. The *Message* virtual class provides the basic interface to package (*Wrap()*) and unpack, (*Unwrap()*) itself. This interface helps approximate Java's I/O offers.

Another class, *TextMessage*, supplies an example of how to use this interface. For example, the *Wrap()* method creates a block of contiguous memory and copies the text into it. (The responsibility of freeing up the block is left to the caller.) The message of *TextMessage* is a variable-length C-style string.