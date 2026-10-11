```
void print(boolean b);
void print(char c);
void print(char[] s);
void print(double d);
void print(float f);
void print(int i);
void print(long l);
void print(Object obj);
void print(String s);
```

Print the designated type. The Object type uses the String.valueOf() method to convert data.

```
void println()
void println(boolean b);
void println(char c);
void println(char[] s);
void println(double d);
void println(float f);
void println(int i);
void println(long l);
void println(Object obj);
void println(String s);
```

Print the designated type and terminate line with newline.
If autoFlush is enabled, flush the stream.

```
void write(int b);
int write(char[] arr);
int write(char[] arr,
int offset, int len);
int write(String s);
int write(String s,
int offset, int len);
```

Write a single byte to the stream.
Write an array of chars (arr) to stream.
Write an array of chars (arr) beginning at offset for len bytes.
Write string to stream.
Write string to stream beginning at offset for len bytes.

Exceptions Thrown:
IOException
SecurityException

# Java Socket Classes

The Java Socket API supports four basic IPv4 classes: Socket, ServerSocket, DatagramSocket, and MulticastSocket. This section describes the interface for each of these classes.