Methods:

| `String getHostAddress();` | Get the numeric address. |
| `byte[] getAddress();` | Get the binary address. |
| `boolean isMulticastAddress();` | Check to see if the address is in the multicast range. |
| `String getHostName();` | Get the host's actual name. |

Exception Thrown:

```
UnknownHostException
```

# # Java I/O Classes

Java has an outstanding set of classes that work with various I/O. Unfortunately, they are not very intuitive, and connecting them together is similar to working with a puzzle. Please read **Chapter 12**, **"Using Java's Networking API"** for more information on how to interlock these pieces into useful streams.

![](bbox=[0.33, 0.37, 0.86, 0.39])

![](bbox=[0.14, 0.4, 0.86, 0.56])

# java.io.InputStream (Abstract Class)

Constructor:

```
InputStream();
```

General Description: A general class for basic stream input.

Parent Class: Object

Methods:

| `int available();` | Return the number of bytes you can read without blocking. |
| `void close();` | Close the channel. |
| `void mark(int readlimit);` | Set the maximum number of bytes to buffer for `mark()` and `reset()`. |
| `boolean markSupported();` | Check to see if stream supports `mark()`/`reset()`. |
| `int read();` | Read a single byte from the stream. |