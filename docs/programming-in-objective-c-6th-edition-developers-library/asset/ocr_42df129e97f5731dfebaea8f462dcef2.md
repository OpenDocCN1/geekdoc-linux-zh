# # The exit() Function

At times, you might want to force the termination of a program, such as when an error condition is detected by a program. You know that program execution is automatically terminated whenever the last statement in main is executed or when executing a return from main. To explicitly terminate a program, no matter from what point you are executing, the exit function can be called. The function call

```
exit (n)
```

has the effect of terminating (exiting from) the current program. Any open files are automatically closed by the system. The integer value n is called the exit status, and has the same meaning as the value returned from main.

The standard header file <stdio.h> defines EXIT_FAILURE as an integer value that you can use to indicate the program has failed and EXIT_SUCCESS to be one that you can use to indicate it has succeeded.

When a program terminates simply by executing the last statement in main, its exit status is undefined. If another program needs to use this exit status, you mustn’t let this happen. In such a case, make certain that you exit or return from main with a defined exit status.

As an example of the use of the exit function, the following function causes the program to terminate with an exit status of EXIT_FAILURE if the file specified as its argument cannot be opened for reading. Naturally, you might want to return the fact that the open failed instead of taking such a drastic action by terminating the program.

Click here to view code image

```
# include <stdio.h>
void checkfile (char *fname) {
FILE *fp;
if ((fp = fopen (fname, "r")) == NULL) {
exit (EXIT_FAILURE);
}
```

Remember that there’s no real difference between exiting or returning from main. They both terminate the program, sending back an exit status. The main difference between exit and return is when they’re executed from inside a function other than main. The exit call terminates the program immediately whereas return simply transfers control back to the calling routine.

# # Renaming and Removing Files

The rename function from the library can be used to change the name of a file. It takes two arguments: the old filename and the new filename. If for some reason the renaming operation fails (for example, if the first file doesn’t exist, or the system doesn’t allow you to rename the particular file), rename returns a nonzero value. The code

Click here to view code image