
## Extra

**FILEMODE ENUMERATION:**

| NAME | DESCRIPTION |
| --- | --- |
| Append | Opens the file if it exists and seeks to the end of the file, or creates a new file. Only works in conjunction with FileAccess.Write. |
| Create | Specifies that the operating system creates a new file. Overwrites the file if it exists. |
| CreateNew | Specifies that the operating system creates a new file. If the file exists, an error occurs. Creates a new file. An error occurs if the file exists. |
| Open | Specifies that the operating system opens an existing file. |
| OpenOrCreate | Specifies that the operating system opens a file if it exists; otherwise creates a new file. |
| Truncate | Specifies that the operating system opens an existing file and clears its contents. |

**FILEACCESS ENUMERATION:**

| NAME | DESCRIPTION |
| --- | --- |
| Read | Opens the file for reading. Allows you to read data from the file. Combine with Write for read/write access. |
| ReadWrite | Opens the file for reading and writing. Allows you to read and write data from the file. |
| Write | Opens the file for writing. Allows you to write data to the file. |

![](img/d6f772854306e15fb6df39b861a7b541_126_0.png)

- 6. Type IO.FileAccess.Read, replacing Read with a constant, which you type or click.
- 7. Type IO.FileShare.ReadWrite), replacing ReadWrite with a constant, which you type or select.
- 8. Type code to access and close the stream.
- 9. Press F5 to run your project.

The FileStream opens or creates the specified file.

## READ FROM A STREAM

A stream provides a conduit to access many different types of data with the same set of methods and properties. For example, the FileStream class enables you to access data in files and the NetworkStream class lets you access data from a network socket. You can use a stream reader to retrieve information from any sort of stream.

The simplest reader, StreamReader, works with textual information and you can use it to read information from a text file.

To declare a new instance of the class, place New in front of the class name and pass the constructor of the StreamReader class an instance of a file stream. For more information on instantiating classes, see Chapter 7.

After creating the reader, call the Read method to retrieve one character out of the stream. Read returns the next available character from the stream as an Integer and moves the current position to the next character. It returns negative one if no more characters remain in the buffer. Use the ReadLine method to read a line out of the text file, return it as a String, and advance the current position to the next line. The ReadToEnd method retrieves all of the data from the current position to the end of the stream and returns it as a String.

The Peek method extracts the character at the current position but does not consume it or advance to the next character position. Like Read, the Peek method returns a negative one if the stream contains no more data. You can use Peek to determine if you have reached the end of the file without reading any data out of it. Always use the Close method after you finish reading from the file to release any resources.

### READ FROM A STREAM

![](img/d6f772854306e15fb6df39b861a7b541_127_0.png)

- 1. Open a method that initializes a stream.
- Note: See the section "Using a File Stream" to create a file stream.
- 2. Type Dim myReader, replacing myReader with the variable name for the reader.
- 3. Type As New IO.StreamReader(myStream), replacing myStream with the name of the Stream.
- 4. Type code to read from the file.
- 5. Press F5 to run the project.

The stream reader processes the text in the file.

## WRITE TO A STREAM

A stream works in two directions, streaming information in and out of your program. You can use a stream writer to output information to a data source. You can use a stream writer to write to a file stream that you open with write access, or write data over a socket connection on a network.

A simple stream writer, the StreamWriter class, provides support for writing textual data. To declare a StreamWriter, use the Dim statement. To declare a new instance of the class, place New in front of the class name and for the most basic constructor, pass the StreamWriter class an instance of a file stream. Chapter 7 provides detailed information on instantiating classes and using constructors.

After you initialize a StreamWriter, the Write method writes a Char, Char array, or a String to the stream but does not move to the next line. The variable passed in is the only parameter. For more information on strings, see Chapter 4. The WriteLine method performs the same action but automatically adds a new line to the file stream.

When you call the Write or WriteLine method, the stream updates in memory only. The Flush method writes any new data you store in the stream to the file. You can write a large amount of information to the stream and flush it to disk in one step. Doing a single large write to disk is more efficient because memory transfers data much faster than disks. If the data needs to move to the disk immediately after calling Write or WriteLine, set StreamWriter.AutoFlush = True.

The Close method closes the writer's connection to the file and removes any resources from memory related to the writing. Unwritten data automatically flushes to the file before the StreamWriter closes.

### WRITE TO A STREAM

![](img/d6f772854306e15fb6df39b861a7b541_128_0.png)

- 1. Open the method that initializes the stream.
- Note: See the section "Using a File Stream" to create a file stream.
- 2. Type Dim myWriter, replacing myWriter with the variable name for the writer.
- 3. Type As New IO.StreamWriter(myStream), replacing myStream with the name of the FileStream.
- 4. Type code to write to the file.
- 5. Press F5 to run the project.

The stream writer outputs text to the file.
