```
```c
n = write(fd, write_buf, sizeof(write_buf));

    if (n!=BUF_SIZE)
        return -1;
    }
}

return i;
}

int write_close(int fd)
{
    if (write_offset>0)
        write(fd, write_buf, write_offset);

    write_offset = 0;
    return close(fd);
}
```
```

This code is only intended to give you the flavor of user buffering because normally you wouldn't write your own - there is a perfectly good user buffering file I/O package in the C standard library (fopen(), fclose() etc.)

Notice that in performing user buffering for writing to files, you encounter the same kind of problems over what to do about reporting errors that we encountered looking at the write() system call itself.

Testing the data transfer rate of the filecopy() function using one byte reads and writes and the user buffering functions gives 330 kilo-bytes per second. As you would expect, this is not as fast as direct large buffer calls to read() and write() because of the overhead of calling the extra functions, but it still shows more than a 50 times' speed improvement over the direct one byte read and write case.

# 15.2 Random Files

All the file access to date has been sequential access by default. This is because all the reads and writes take place starting from the current file offset position. The file offset value is then automatically incremented to just beyond the position where the read or write finishes, which makes it ready for the next access to take place.

Given this scenario, random access under Linux couldn't be simpler. All you need to do is to alter the current file offset value to the position of interest which will automatically force the next read() or write() to take place at this position (unless the file was opened O_APPEND of course, in which case any write() calls will still take place at the end-of-file position).