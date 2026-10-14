It might surprise you that C++ has no native capabilities for input and output (I/O). The same is true of C. In both languages, I/O is provided strictly by library functions. For instance, to read and write data in C++ programs—whether to and from the console, or in a disk file—you must include the iostream.h header file and link the program to the compiled I/O stream library.

Not having I/O facilities built into a programming language might seem to be a drawback, but because I/O in C and C++ is provided by compiled libraries, programmers who develop code for embedded systems or for special-purpose computers are free to devise their own I/O functions and techniques. This fact makes C and C++ well suited to low-level programming. However, most software application developers might as well take advantage of the standard libraries. They have been tweaked to the hilt by GNU's authors, and it would be difficult to outdo their efforts.

This chapter explains how to read and write fundamental data objects and strings using C++ I/O streams, and how to format strings to produce good-looking output.

# INTRODUCING C++ I/O STREAMS

An I/O stream object behaves much like the standard input and output file streams that are familiar to C programmers. But rather than call a standard library function such as puts(), C++ programs use the "put-to" operator (<<) for output and the "get-from" operator (>>) for input operations. For example, in C++, to write a program's title string to the standard output, you can use a statement such as

```
cout << "Fishbowl Screen Saver by Grouper Tom" << endl;
```

You've seen similar statements many times so far in this book. However, the cout object also provides functions you can call to perform many different tasks. To write a single character variable c to the standard output, you can use the statements:

```
char c = 'p';
cout.put(c);
```

The put() function is a member of the cout object's class—a new concept that you learn more about in Chapter 12, "Introducing the Class." To call an object's member function, type a period after the object name followed by the function to call. The function is called in reference to its object, in this case, cout.

Similarly, to read a character from the standard input, use the input stream object, cin, along with the get-from operator, >>. This statement reads one character from the standard input into a char variable c:

```
char c;
cin >> c;
```

Notice that the put-to and get-from operators seem to point to their targets. As you can with cout, you can call a member function in reference to cin. For example, the following performs the identical task as the preceding statement:

```
cin.get(c);
```