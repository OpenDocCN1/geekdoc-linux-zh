If your site is using its own translations of the message catalogs, consult your system administrator for the appropriate value of NLSPATH or LANG. For additional information on NLS and message catalogs, see AIX General Programming Concepts: Writing and Debugging Programs.

# ## Dealing with Errors

At run time, you can encounter a number of different types of errors that are specifically related to the use of the ESSL subroutines:

+   - Program exceptions
+   - Input-argument errors (2001-2099) and (2200-2299)
+   - Computational errors (2100-2199)
+   - Resource errors (2401-2499)
+   - Informational and Attention messages (2600-2699)
+   - Miscellaneous errors (2700-2799)

# ## Program Exceptions

The program exceptions you can encounter in ESSL are described in ANSI/IEEE Standard for Binary Floating-Point Arithmetic, ANSI/IEEE Standard 754-1985.

# ## ESSL Input-Argument Error Messages

If you receive an error message in the form 2538-20nn or 2538-22nn, you have an input-argument error in the calling sequence for an ESSL subroutine. Your program terminated at this point unless you did one of the following:

+   - Specified the ESSL user exit routine, ENOTRM, with ERRSET to determine the correct input argument values in your program for the optionally-recoverable ESSL errors 2015, 2030 or 2200. For details on how to do this, see Chapter 4, “Coding your Program,” on page 107.
+   - Reset the number of allowable errors (2099) during ESSL installation or using ERRSET in your program. This is not recommended for input-argument errors.

Note: For many of the ESSL subroutines requiring auxiliary storage, you can avoid program termination due to error 2015 by allowing ESSL to dynamically allocate auxiliary storage for you. You do this by setting nux = 0 and making error 2015 unrecoverable. For details on which nux arguments allow dynamic allocation and how to specify this, see the subroutine descriptions in Part 2 of this book.

The name of the ESSL subroutine detecting the error is listed as part of the message. The argument number(s) involved in the error appears in the message text. See “Input-Argument Error Messages(2001-2099)” on page 176 for a complete description of the information contained in each message and for an indication of which messages correspond to optionally-recoverable errors. Regardless of whether the name in the message is a user-callable ESSL subroutine or an internal ESSL routine, the message-text and its unique parts apply to the user-callable ESSL subroutine. Return code values are described under “Error Conditions” for each ESSL subroutine in Part 2 of this book.

You may get more than one error message, because most of the arguments are checked by ESSL for possible errors during each call to the subroutine. The ESSL subroutine returns as many messages as there are errors detected. As a result, fewer runs are necessary to diagnose your program.