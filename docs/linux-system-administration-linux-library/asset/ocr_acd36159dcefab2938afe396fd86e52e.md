In contrast to hard links, a symbolic link can be used to link directories. If you move or delete the linked-to file, the symbolic link will be left "dangling", pointing at nothing, unlike a hard link in which the file contents would still exist and be accessible from the link. If you delete a symbolic link, re-creating a new file of the link's name won't auto-matically restore the link; you must use the `~i` command again to re-create the link.

# Pipes

A named pipe, also called a FIFO (first in, first out), is a special file type that allows independent processes to communicate with each other. The first process opens a specified file—pipe—for writing. The other opens the same file for reading. The processes communicate via that file. All communication between the process and the pipe is undirectional. Each time the file is opened, for reading or writing, the open function blocks other processes from opening the same pipe for the same activity. That is, if the pipe is opened for read-only, the open function will not return, thereby blocking any requests to open that pipe for read-only; attempts to open the pipe for writing will cause the open for read-only to terminate. If, on the other hand, the pipe is opened for writing, all attempts to open the same pipe for writing will be blocked, but the first attempt to open it for reading will be allowed. The rules for blocking are as follows:

+   - If you open the pipe for both reading and writing, then the open function will not perform blocking.
- If you open the pipe for reading, the open function will not return until another process opens the FIFO for writing, unless `O_NONBLOCK` is specified, in which case the open succeeds.
- If you are writing for writing, the open function will not return until another process opens the FIFO for reading, unless `O_NONBLOCK` is specified, in which case the open fails.

For example, suppose you want to display a daily fortune using `.signature` file. You could use the name of that file as a pipe from a fortune-generating program. Now every time any program tries to read from your `.signature` file, the reading program will pause your program to supply a fortune as your `.signature`.

The specifics for reading and writing using named pipes require programming functions which are beyond the scope of this book. The creation of a named pipe, however, is very much part of a system administrator's job. There are two ways to create a named pipe: using the `mkfifo` command or using the `mkknod` command if `mkfifo` isn't available. The two commands each create a named pipe called `test_fifo:`

```
$ mkfifo test_fifo
```

```
$ mkknod test_fifo p
```