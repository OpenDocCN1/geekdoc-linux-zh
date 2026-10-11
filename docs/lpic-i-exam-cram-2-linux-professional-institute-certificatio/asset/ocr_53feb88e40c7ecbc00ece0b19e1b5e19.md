disposal—in other words, a pseudo-device designed to be a place to discard data securely.

# # Redirection of Streams

In the quest for good data, being able to redirect or change the destination of `stdout` and `stderr`, and to some degree `stdin`, is essential to your tasks.

Redirection symbols include

+   ▶ - Redirects a file’s contents into a command’s `stdin` stream. The file descriptor for the `<` input redirection symbol is `0`.

+   ▶ - Redirects the `stdout` stream to the file target to the right of the symbol. The file descriptor for the `>` output redirection character is `1`, which is implied, except in certain instances.

+   ▶ - Redirects `stdout` to a file, appending the current stream to the end of the file, rather than overwriting the file contents. This is a modifier of the `>` output redirection descriptor.

> If using the `>` redirection symbol to write to a file, that fill is overwritten unless the `noclobber` bash shell option is set. With that option set, you cannot overwrite the file; it will produce an error and file. The only way to get data into that file is to use the `>>` redirection append symbols.

# # Redirecting Standard Input

Redirecting `stdin` consists of sending a file’s contents to a program’s `stdin` stream. An example of this is

```
`sort < file1`
```

Although it might seem odd to have a couple of ways to do the same thing, the previous command is essentially the same as the following command:

```
`cat file1 | sort`
```

# # Redirecting Standard Output

Redirecting `stdout` consists of either a single redirection symbol (>) or two (>>) for appending. The main difference is that the use of a single redirection descriptor overwrites a file whereas using double redirection descriptors appends to the end of a file, like so:

```
`cat file1 > file2`
```