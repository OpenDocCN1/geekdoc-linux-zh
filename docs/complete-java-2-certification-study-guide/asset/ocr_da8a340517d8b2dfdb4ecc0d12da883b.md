the file is opened for reading and writing, and changes to the file content, but not to its metadata,
take place immediately.

The second form of the constructor is useful when you want to use some of the methods of the
File class before opening a random-access file, so that you already have an instance of File at
hand when it comes to call the RandomAccessFile constructor. For example, the following
code constructs an instance of File to verify that the string path represents a
file that exists and may be written. If this is the case, the RandomAccessFile constructor is called;
otherwise an exception is thrown:

+   1. File file = new File(path);
2. if (file.isFile()) ||
3. if (file.canRead()) ||
4. if (file.canWrite())
5. throw new IOException();
6. RandomAccessFile raf = new RandomAccessFile(file, "rw");

When the named file does not exist, constructing a RandomAccessFile is different from
structuring an ordinary File. In this situation, the random-access file is constructed in read-only
mode, a FileNotFoundException is thrown. If the random-access file is constructed in read-
write mode, then a zero-length file is created.

After a random-access file is constructed, you can seek to any position within the file and
then read or write. Pre-Java systems (the C standard I/O library, for example) have supported
seeking to a position relative to the beginning of the file, the end of the file, or the current position
within the file. Java's random-access files support only seeking relative to the beginning of the file;
but methods exist that report the current position and length of the file, so you can effectively\perform the other kinds of seeking as you are willing to do the arithmetic.
The methods that support seeking are as follows:

```
long getPointer() throws IOException Returns the current position within the
file, in bytes. Subsequent reading and writing will take place starting at this position.
```

```
long length() throws IOException Returns the length of the file, in bytes.
```

```
void seek(long position) throws IOException Sets the current position within the
file, in bytes. Subsequent reading and writing will take place starting at this position. Files
at 0.
```

The following is a subclass of RandomAccessFile that adds two new methods to sup-
port seeking from the current position or the end of the file. The code illustrates the use of the
methods just listed:

```
import java.io.*;
```

```
class GeneralRAF extends RandomAccessFile {
    public GeneralRAF(File path
```