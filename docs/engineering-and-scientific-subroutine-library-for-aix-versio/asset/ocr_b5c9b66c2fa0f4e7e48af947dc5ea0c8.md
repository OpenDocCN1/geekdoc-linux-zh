![](bbox=[0.1, 0.09, 0.85, 0.54])

*Figure 9. How to Obtain Computational Error Information in an Error Message and in Your Program*

# What Can You Do about ESSL Resource Errors?

This section gives an overview on how you can handle resource errors.

# All Resource Errors

ESSL returns a resource error and terminates your program when an attempt to allocate work area fails. Some ESSL subroutines attempt to allocate work area for their internal use. Other ESSL subroutines attempt to dynamically allocate auxiliary storage when a user requests it through calling sequence arguments, such as *aux* and *naux*. For information on how you could reduce memory constraints on the system or increase the amount of memory available before rerunning the application program, see “ESSL Resource Error Messages” on page 172.

You can determine the resource errors that can occur in a subroutine by looking under “Error Conditions” in the subroutine description in Part 2 of this book. Error messages for all resource errors are listed in “Resource Error Messages(2400-2499)” on page 184.

# What Can You Do about ESSL Attention Messages?

This section gives an overview on how you can handle attention messages.