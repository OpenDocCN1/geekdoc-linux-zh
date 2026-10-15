When the argument to ls is a non-directory file, it may have to obtain the attributes of the file and display them. When the argument is a directory, say dir, ls has to do something like

```
open the directory dir
while not all directory entries in dir have been read
    read the entry
        optionally display information about the entry
close the directory
```

The questions are, how can we open, read, and close a directory, and how can we obtain information about file attributes. Fortunately none of these tasks are particularly difficult, owing to the simplicity of the file system interface.

# 3.8  The Directory Interface

Recall that, as far as the kernel is concerned, regular files are just sequences of bytes. Directories are like regular files except that

+   1. They are never empty:
+   
+      Directories are not empty because every directory has two unique entries, “.” and “..” that refer respectively to the directory itself and to the parent directory. These are created when the directory is created.
+   
+   2. They cannot be written to by unprivileged programs:
+   
+      They can only be modified by very specific system calls, unlike regular files. In contrast, anyone with appropriate permission may read the contents of a directory. Some commands that operate on regular files can be applied to directories, but with unexpected results.
+   
+   3. They have a specific structure:
+   
+      A directory is a file that contains a collection of (name, i-number) pairs. In other words, a directory is a table of records. You can think of it as a hash table, since it is accessed with a name in order to retrieve the i-number.

Some commands that read files also read directories, but the results are not useful. For example, on some systems, the cat command and the od command may display the contents of a directory as a stream of bytes, but because a directory is not a text file, the output of cat will look garbled. The output of od may look normal. Usually, these commands, like the more command, check whether their argument is a directory, and if so, refuse to execute, displaying instead an error message:

```
$ more projects
*** projects: Is a directory ***
```

The more command refused to display projects because it is a directory and a directory displayed as a sequence of characters would not be meaningful. The output of od may reveal the structure of the directory to you if you really examine it carefully. The -c option to od displays bytes that can