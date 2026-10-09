| `int read()`; `int read(byte[]) arr, int offset, int len);` `readFully(byte[]) arr); readFully(byte[]) arr, int offset, int len);` | Read a byte or an array of bytes beginning at offset for len bytes. readFully() reads all the bytes to fill the array, blocking as needed. |
| `boolean readBoolean();` `byte readByte();` `char readChar();` `double readDouble();` `float readFloat();` `int readInt();` `long readLong();` `short readShort();` `int readUnsignedByte();` `int readUnsignedShort();` | Read the designated type. |
| `String readUTF();` `Object readObject();` | Read Object instance. You can discover the type and then convert it later with the casting operators. |

# Exceptions Thrown:

+   - IOException
- ClassNotFoundException
- NotActiveException
- OptionalDataException
- InvalidObjectException
- SecurityException
- StreamCorruptedException

# java.io.OutputStream (Abstract Class)

Constructor:

```
OutputStream();
```

General Description: A general class for basic stream input.

Parent Class: Object

Methods:

| `void close();` | Close the channel. |
| `void flush();` | Flush written data from buffers. |
| `void write(byte b);` | Write a single byte to the stream. |
| `int write(byte[]) arr);` | Write an array of bytes (arr) to the stream. |
| `int write(byte[]) arr, int offset, int len);` | Write an array of bytes (arr) beginning at offset for len bytes. |

# Exception Thrown:

+   - IOException