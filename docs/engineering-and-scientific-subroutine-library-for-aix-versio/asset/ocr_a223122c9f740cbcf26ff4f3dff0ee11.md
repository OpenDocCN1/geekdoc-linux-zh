Restoring Entries in the Error Option Table?” For how to use ERRSAV and ERRSTR, see the section for your programming language in Chapter 4, “Coding Your Program,” on page 107.

# How Can You Control Error Handling in Large Applications by Saving and Restoring Entries in the Error Option Table?

When your program is part of a larger application, you should consider that one of the following can occur:

+   - If you use ERRSET in your program to reset any of the values in the error option table for any of the ESL input-argument errors or computational errors, some other program in the application may be adversely affected. It may be expecting its original values.

+   - If some other program in the application uses ERRSET to reset any of the values in the error option table for any of the ESL input-argument errors or computational errors, your program may be adversely affected. You may need a certain value in the error option table, and the application may have reset that value.

These situations can be avoided if every program that uses ERRSET, in the large application, also uses the ERRSAV and ERRSTR facilities. For a particular error number, ERRSAV saves an entry from the error option table in an area accessible to your program. ERRSTR then stores the entry back into the error option table from the storage area. You code an ERRSAV and ERRSTR for each input-argument error number and computational error number for which you do an ERRSET to reset the values in the error option table. Call ERRSAV at the beginning of your program after you call EINFO, and then call ERRSTR at the end of your program after all ESL computations are completed. This saves the original contents of the error option table while your program is running with different values, and then restores it to its original contents when your program is done. For details on how to code these statements in your program, see Chapter 4, “Coding Your Program,” on page 107.

# How does Error Handling Work in a Threaded Environment?

When your application program or Fortran first creates a thread, ESL initializes the error option table information to the default settings shown in Table 29 on page 50. You can change the default settings for each thread you created by calling the appropriate error handling subroutines (ERRSET, ERRSAV, or ERRSTR) from each thread. An example of how to initialize the error option table and change the default settings on multiple threads is shown in “Example of Handling Errors in a Multithreaded Application Program” on page 122.

ESL issues error messages as they occur in a threaded environment. Error messages issued from any of the existing threads are written to standard output in the order in which they occur.

When a terminating condition occurs on any of the existing threads (for example, the number of allowable errors was exceeded), ESL terminates your application program. One set of summary information corresponding to the terminating thread is always printed. Summary information corresponding to other threads may also be printed.

# Where Can You Find More Information on Errors?

Information about errors and how to handle them can be found in the following places: