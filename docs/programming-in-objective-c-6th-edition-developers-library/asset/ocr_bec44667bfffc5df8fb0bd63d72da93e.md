writing, "          for appending to the end of an existing file, "          for read/write access starting at the beginning of an existing file, "          for read/write access (and the previous contents of the file, if it exists, are lost), and "          for read/write access with all writes going to the end of the file. If the file to be opened does not exist, it is created if the *accessMode* is write ("          ", "          ") or append ("          ,          "). If a file is opened in append mode ("          " or "          "), it is not possible to overwrite existing data in the file.

On systems that distinguish binary from text files, the letter b must be appended to the access mode (as in "          ") to open a binary file.

If the f          call is successful, a F          pointer is returned to be used to identify the file in subsequent I/O operations; otherwise, a null pointer is returned.

Click here to view code image

```
i                       *filePtr, format, arg1, arg2, ..., argn)
```

Writes the specified arguments to the file identified by *filePtr*, according to the format specified by the character string *format*. Format characters are the same as for the p          function (see Chapter 15, "Input and Output Operations in C"). The number of characters written is returned. A negative return value indicates that an error occurred on output.

```
i                   c, *filePtr)
```

Writes the value of c (converted to an u          ) to the file identified by *filePtr*, returning c if the write is successful, and the value E          otherwise.

```
i                    buffer, *filePtr)
```

Writes the characters in the array pointed to by *buffer* to the indicated file until the terminating null character in *buffer* is reached. A newline character is *not* automatically written to the file by this function. On failure, the value E          is returned.

Click here to view code image

```
s                       buffer, size, n, *filePtr)
```

Reads n items of data from the identified file into *buffer*. Each item of data is *size* bytes in length. For example, the call

Click here to view code image

```
n
```

reads 80 characters from the file identified by i          and stores them into the array pointed to by t          . The function returns the number of data items successfully read.

Click here to view code image

```
F                    fileName, accessMode, *filePtr)
```

Closes the file associated with *filePtr* and opens the file *fileName* with the specified *accessMode* (see the f          function). The file that is opened is subsequently associated with *filePtr*. If the f          call is successful, *filePtr* is returned; otherwise, a null pointer is returned. The f          function is frequently used to reassign s          , s          , or s          in the program. For example, the call