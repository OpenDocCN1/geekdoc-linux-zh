# ERRSAV—ESSL ERRSAV Subroutine for ESSL

The ERRSAV subroutine copies an ESSL error option table entry into an 8-byte storage area that is accessible to your program.

For multithreaded application programs, if you want the error handling capabilities that this subroutine provides to be implemented on each thread created by your program, this subroutine must be called from each thread. If your application creates multiple threads, the action performed by a call to this subroutine applies to the thread that this subroutine was invoked from. For an example, see “Example of Handling Errors in a Multithreaded Application Program” on page 122.

# Syntax

| Language | Syntax |
| :--- | :--- |
| Fortran | CALL ERRSAV (ierno, tabent) |
| C and C++ | errsav (ierno, tabent); |

# On Entry:

*ierno*

is the error number in the option table. The entry for *ierno* in the ESSL error option table is stored in the 8-byte storage area *tabent*.

Specified as: a fullword integer; *ierno* must be one of the error numbers in the option table. For a list of these numbers, see Table 29 on page 50.

# On Return:

*tabent*

is the storage area where the option table entry is stored.

Specified as: an area of storage of length 8-bytes.

# Note

Examples of how to use ERRSAV are provided in Chapter 4, “Coding Your Program,” on page 107.