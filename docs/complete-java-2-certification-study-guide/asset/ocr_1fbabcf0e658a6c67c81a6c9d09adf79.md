# Chapter 9 • I/O and Streams

int read(byte[], int offset, int len) throws IOException Attempts to read
len bytes into array[], starting at offset. It returns the number of bytes read or -1 if at
end of the file.

The following code fragment illustrates the use of these methods by reading a single stream into
byte, then enough to fill byte array[], and finally 20 bytes into the first 20 loca-
tions of byte array morebytes[];

```
byte b;
byte bytes[] = new byte[100];
byte morebytes[] = new byte[50];
try {
    InputStream fis = new FileInputStream("fname");
    b = (byte) fis.read();      // Single byte
    fis.read(bytes);            // Fill the array
    fis.read(morebytes, 0, 20); // 1st 20 bytes
    fis.close();
}
catch (IOException e) {
```

The FileInputStream class has a few useful utility methods:

int available() throws IOException Returns the number of bytes that can be read
without blocking.

void close() throws IOException Releases non-memory system resources associated
with the file. A file stream should always be closed when no longer needed.

long skip(long nbytes) throws IOException Attempts to read and discard nbytes
bytes. Returns the number of bytes actually skipped.

It is not surprising that output streams are almost identical to file input streams. The com-
used constructors are

+   - FileOutputStream(String pathname)
- FileStream(File file)

There are methods to support writing a single byte, an array of bytes, or a subset of an array of bytes:

void write(int b) throws IOException Writes the low-order byte of b.

void write(byte bytes[]) throws IOException Writes all members of byte array
bytes].

void write(byte bytes[], int offset, int len) throws IOException Writes len
from array bytes[], starting at offset.

The OutputStream class also has a close() method, which should always be called
when a file stream is no longer needed.