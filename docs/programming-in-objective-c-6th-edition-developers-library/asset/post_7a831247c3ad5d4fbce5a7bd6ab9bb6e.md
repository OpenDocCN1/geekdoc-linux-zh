
not the same as telling you that you just read the last data item from a file. You have to read one past the last data item for `f` to return nonzero.

### The `fprintf( )` and `fscanf( )` Functions

The functions `fprintf( )` and `fscanf( )` are provided to perform the analogous operations of the `printf( )` and `scanf( )` functions on a file. These functions take an additional argument, which is the `FILE` pointer that identifies the file to which the data is to be written or from which the data is to be read. So, to write the character string "Hello!" into the file identified by `of`, you can write the following statement:

```C
fprintf( of, "Hello!\n" );
```

Similarly, to read in the next floating-point value from the file identified by `if` into the variable `f`, the statement

```C
fscanf( if, "%f", &f );
```

can be used. As with `scanf( )`, `fscanf( )` returns the number of arguments that are successfully read and assigned or the value `EOF`, if the end of the file is reached before any of the conversion specifications have been processed.

### The `fgets( )` and `fputs( )` Functions

For reading and writing entire lines of data from and to a file, the `fgets( )` and `fputs( )` functions can be used. The `fgets( )` function is called as follows:

```C
fgets( buffer, n, filePtr )
```

`buffer` is a pointer to a character array where the line that is read in will be stored; `n` is an integer value that represents the maximum number of characters to be stored into `buffer`; and `filePtr` identifies the file from which the line is to be read.

The `fgets( )` function reads characters from the specified file until a newline character has been read (which *will* get stored in the buffer) or until *n*-*l* characters have been read, whichever occurs first. The function automatically places a null character after the last character in `buffer`. It returns the value of `buffer` (the first argument) if the read is successful, and the value `NULL` if an error occurs on the read or if an attempt is made to read past the end of the file.

The `fputs( )` function can be combined with `scanf( )` (see Appendix B, “The Standard C Library”) to perform line-oriented reading in a more orderly and controlled fashion than by using `scanf( )` alone.

The `fputs( )` function writes a line of characters to a specified file. The function is called as follows:

```C
fputs( buffer, filePtr )
```

### *stdin, stdout, and stderr*

When a C program is executed, three files are automatically opened by the system for use by the program. These files are identified by the *constant FILE* pointers `stdin`, `stdout`, and `stderr`, which are defined in `<stdio.h>`. The `FILE` pointer `stdin` identifies the standard input of the program and is normally associated with your terminal window. All standard I/O functions that perform input and do not take a `FILE` pointer as an argument get their input from `stdin`. For example, the `scanf` function reads its input from `stdin`, and a call to this function is equivalent to a call to the `fscanf` function with `stdin` as the first argument. So, the call

```C
scanf( "%d", &i );
```

reads in the next integer value from the standard input, which is normally your terminal window. If the input to your program has been redirected to a file, this call reads the next integer value from the file to which the standard input has been redirected.

As you might have guessed, `stdout` refers to the standard output, which is normally also associated with your terminal window. So, a call such as

```C
printf( "Hello\n" );
```

can be replaced by an equivalent call to the `fprintf` function with `stdout` as the first argument:

```C
fprintf( stdout, "Hello\n" );
```

The `FILE` pointer `stderr` identifies the standard error file. This is where most of the error messages produced by the system are written and is also normally associated with your terminal window. The reason `stderr` exists is so that error messages can be logged to a device or file other than where the normal output is written. This is particularly desirable when the program's output is redirected to a file. In such a case, the normal output is written into the file, but any system error messages still appear in your window. You might want to write your own error messages to `stderr` for this same reason. As an example, the `fprintf` call in the following statement:

```C
fprintf( stderr, "Cannot open file\n" );
```

writes the indicated error message to `stderr` if the file `d` cannot be opened for reading. In addition, if the standard output has been redirected to a file, this message still appears in your window.

## The `exit( )` Function

At times, you might want to force the termination of a program, such as when an error condition is detected by a program. You know that program execution is automatically terminated whenever the last statement in `main` is executed or when executing a `return` from `main`. To explicitly terminate a program, no matter from what point you are executing, the `exit` function can be called. The function call

```C
exit( n );
```

has the effect of terminating (exiting from) the current program. Any open files are automatically closed by the system. The integer value `n` is called the exit status, and has the same meaning as the value returned from `main`.

The standard header file `<stdio.h>` defines `EXIT_FAILURE` as an integer value that you can use to indicate the program has failed and `EXIT_SUCCESS` to be one that you can use to indicate it has succeeded.

When a program terminates simply by executing the last statement in `main`, its exit status is undefined. If another program needs to use this exit status, you mustn’t let this happen. In such a case, make certain that you exit or return from `main` with a defined exit status.

As an example of the use of the `exit` function, the following function causes the program to terminate with an exit status of `EXIT_FAILURE` if the file specified as its argument cannot be opened for reading. Naturally, you might want to return the fact that the open failed instead of taking such a drastic action by terminating the program.

```C
#include <stdio.h>
void checkfile( char *fname ) {
    FILE *fp;
    if( (fp = fopen( fname, "r" )) == NULL )
        exit( EXIT_FAILURE );
}
```

Remember that there’s no real difference between exiting or returning from `main`. They both terminate the program, sending back an exit status. The main difference between `exit` and `return` is when they’re executed from inside a function other than `main`. The `exit` call terminates the program immediately whereas `return` simply transfers control back to the calling routine.

## Renaming and Removing Files

The `rename` function from the library can be used to change the name of a file. It takes two arguments: the old filename and the new filename. If for some reason the renaming operation fails (for example, if the first file doesn’t exist, or the system doesn’t allow you to rename the particular file), `rename` returns a nonzero value. The code

```C
if( rename( "t", "d" ) != 0 )
    fprintf( stderr, "Rename failed\n" );
```

renames the file called `t` to `d` and checks the result of the operation to ensure it succeeded.

The `remove` function deletes the file specified by its argument. It returns a nonzero value if the file removal fails. The code

```C
if( remove( "t" ) != 0 ) {
    fprintf( stderr, "Remove failed\n" );
    exit( EXIT_FAILURE );
}
```

attempts to remove the file `t` and writes an error message to standard error and exit if the removal fails.

Incidentally, you might be interested in using the `perror` function to report errors from standard library routines. For more details, consult *Appendix B*.

This concludes our discussion of I/O operations under C. As mentioned, not all of the library functions are covered here due to lack of space. The standard C library contains a wide selection of functions for performing operations with character strings, for *random I/O*, mathematical calculations, and dynamic memory management. *Appendix B* lists many of the functions inside this library.

## Exercises

- 1. Type in and run the three programs presented in this chapter. Compare the output produced by each program with the output presented in the text.

- 2. Go back to programs developed earlier in this book and experiment with redirecting their input and output to files.

- 3. Write a program to copy one file to another, replacing all lowercase characters with their uppercase equivalents.

- 4. Write a program that merges lines alternately from two files and writes the results to *s*. If one file has fewer lines than the other, the remaining lines to the larger file should simply be copied to *s*.

- 5. Write a program that writes columns *m* through *n* of each line of a file to *s*. Have the program accept the values of *m* and *n* from the terminal window.

- 6. Write a program that displays the contents of a file at the terminal 20 lines at a time. At the end of each 20 lines, have the program wait for a character to be entered from the terminal. If the character is the letter q, the program should stop the display of the file; any other character should cause the next 20 lines from the file to be displayed.
