file size. Read the man page for the du command to determine the block size used so you can perform this task. Now verify that the bigdata file contains holes equal to 28K bytes.

# 18. What is the purpose of the following program? Explain your answer.

```
int main(void)
{
    int nr, nw;
    while ((nr = read(0, &c, 1)) != 0)
        nw = write(1, &c, 1);
    return(0);
}
```

# 19. Write a C program that takes a file as a command line argument and outputs Yes if the file is empty and No if it isn't. Show the source code, compilation of the source code, and a few sample runs of the program.

# 20. What would happen if we did not use the O_TRUNC flag in the cpy.c program in Section 18.8.4?

# 21. Modify the truncate.c program discussed in Section 18.8.6 so that it takes any number of files as command line arguments and truncates them to the argument specified as the last argument. It displays the names and sizes of the original and truncated files in the form of a table and removes the truncated files from the file system. Show a few sample runs of the program.

# 22. Change the truncate.c program discussed in Section 18.8.6 so that it takes three command line arguments. The first two arguments are file names, with the first the name of an existing file. The third argument specifies the new file length. The program creates the file with the name given as the second argument, copies the first file into it, truncates the file according to the third argument, displays the sizes of the original and truncated file, removes the truncated file from the file system, and terminates. Show a few sample runs of the program.

# 23. Browse through the <stdio.h> file and identify the values (or macros) for the following:

+   - Maximum number of files that the system allows to be opened concurrently
+   - Macros for standard files
+   - Macros that define SEEK_CUR, SEEK_END, and SEEK_SET

# 24. Browse through the <stdio.h> file and identify all of the functions and their purposes.

# 25. Write a program that opens a file with one hard link and removes the file with the unlink() system call. Read data from the opened file and send it to standard output using the write() system call. What happens? Is your program able to read file data? Explain your answer.