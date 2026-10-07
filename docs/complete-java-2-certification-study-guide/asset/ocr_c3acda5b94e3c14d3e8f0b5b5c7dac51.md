```
// Close the chain
dos.close();
fos.close();
}
catch (IOException e) { }
```

In addition to data input streams and output streams, the java.io package offers several other high-level stream classes. The constructors for all high-level input streams require you to pass in the next-level input stream in the chain; it will be the source of data read by the new object. Similarly, the constructors for the high-level output streams require you to pass in the next-lower output stream in the chain; the new object will write data to this. Some of the high-level streams are listed here:

**BufferedInputStream and BufferedOutputStream** These classes have internal buffers that bytes can be read or written in large blocks, minimizing I/O overhead.

**PrintStream** This class can be asked to write text or primitives. Primitives are converted to character representations. The System.out and System.err objects are examples of this class. The class has a println() method that outputs a string followed by a newline character. It also has a format() method that prints formatted text. Text formatting is covered in Chapter 8, java.lang and java.util packages.

**PushbackInputStream** This class allows the most recently read byte to be put back into the stream, as if it had not yet read before. This functionality is very useful for certain kinds of parsers.

It is possible to create stream chains of arbitrary length. For example, the following code fragment implements a data input stream that reads from a buffered input stream, in which it reads from a file input stream:

```
FileInputStream f = new FileInputStream('text');
BufferedInputStream b = new BufferedInputStream(f);
DataInputStream d = new DataInputStream(b);
```

The chain that this code creates is shown in Figure 9.

# Readers and Writers

Readers and writers are like input and output streams. The low-level varieties communicate with I/O devices, and the high-level varieties communicate with low-level varieties. What makes readers and writers different is that they are exclusively oriented to Unicode characters.