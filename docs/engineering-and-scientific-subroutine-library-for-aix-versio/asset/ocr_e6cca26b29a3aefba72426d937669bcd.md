.RCFT and _CRT. Using these stride values for your data allows the Fourier transform subroutines to achieve maximum performance. You first obtain the optimal stride values from STRIDE, calling it once for each stride value desired. You then arrange your data using these stride values. After the data is set up, you call the Fourier transform subroutine. For details on the STRIDE subroutine and how to use it for each Fourier transform subroutine, see “STRIDE—Determine the Stride Value for Optimal Performance in Specified Fourier Transform Subroutines” on page 963. For additional information, see “Setting Up Your Data” on page 746.

# Where Can You Find More Information on Performance?

+   - Many of the techniques ESSL uses to achieve the best possible performance are described in the “High Performance of ESSL” on page 6.
+   - Migration considerations concerning performance are described in Chapter 6, “Migrating Your Programs,” on page 165.
+   - Specific information on performance for each area of ESSL is given in “Performance and Accuracy Considerations” in each chapter introduction in Part 2.
+   - Detailed performance information for selected subroutines can be found in reference [32], [43], [44].

# Dealing with Errors when Using ESSL

+   - Program exceptions
+   - ESSL input-argument errors
+   - ESSL computational errors
+   - ESSL resource errors
+   - ESSL attention messages

At run time, you can encounter different types of errors or messages that are related to the use of the ESSL subroutines:

This section explains how to handle all these situations.

# What Can You Do about Program Exceptions?

The program exceptions you can encounter in ESSL are described in the ANSI/IEEE Standard for Binary Floating-Point Arithmetic, ANSI/IEEE Standard 754-1985.

# What Can You Do about ESSL Input-Argument Errors?

This section gives an overview on how you can handle input-argument errors.

# All Input-Argument Errors

ESSL checks the validity of most input arguments. If it finds that any are invalid, it issues the appropriate error messages. Also, except for the three recoverable errors described below, it terminates your program. You should use standard programming techniques to diagnose and fix unrecoverable input-argument errors, as described in Chapter 7, “Handling Problems,” on page 169.

You can determine the input-argument errors that can occur in a subroutine by looking under “Error Conditions” in the subroutine description in Part 2 of this book. Error messages for all input-argument errors are listed in “Input-Argument Error Messages(2001-2099)” on page 176.