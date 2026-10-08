```
static_cast<data_type>(expression)
```

# reinterpret_cast

A reinterpret_cast operator converts a type into a fundamentally different type. For example, it can change a pointer into an integer and vice versa. It can also be used to cast incompatible pointer types. The format of a reinterpret_cast is:

```
reinterpret_cast<data_type>(expression)
```

# Exception Handling

An exception is an error that occurs at runtime. C++ allows pro-grammers to handle runtime exceptions in a controlled manner. Errors or exceptions can be caught and handled easily with an error handling routine.

There are three keywords for exception handling: try, catch, and throw. Programming statements to be monitored are contained in a try block. If an exception occurs within the try block, it is thrown using throw. The exception is caught using catch and is processed by an error-handling routine.

The throw generates an exception based upon the error encountered. The throw is executed from within a try block or from a function within the try block. The format for a throw statement is:

```
throw exception;
```

The general form of a try and catch is:

```
try
{
// statements to check for errors - try block
```