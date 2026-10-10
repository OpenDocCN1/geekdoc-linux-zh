here is that if you want to have the updated argument value returned to your program, you must make error 2015 recoverable and then specify an \textit{nux} value greater than or equal to 20 and less than 300. For values out of that range, the error recovery facility is not in effect. (These values of \textit{nux}, 20 and 300, are used only for the purposes of this example and do not relate to any of the ESSL subroutines.)

+   NAUX  Meaning of the NAUX Value
+   20  Lower limit of \textit{nux} required for using recoverable input-argument error-handling facilities in ESSL. (This applies only to several \textit{nux1} arguments in the Fourier transform, convolution, and correlation subroutines. You can find the lower limit in the syntax description for the \textit{nux1} argument. For a list of subroutines, see Table 25 on page 32.)
+   300  Minimum value of \textit{nux}, required for successful running (on the processor the program is being run on).

Table 26 describes the actions taken by ESSL in every possible situation for the values given in this example.

**Table 26.** *Example of Input-Argument Error Recovery for Auxiliary Storage Sizes*
|NAUX Value|Action When 2015 Is an Unrecoverable Input-Argument Error|Action When 2015 Is a Recoverable Input-Argument Error|
|*naux* < 20|An input-argument error message is issued. The value in the error message is the lower limit, 20. The application program stops.|An input-argument error message is issued. The value in the error message is the lower limit, 20. The application program stops.|
|20 \leq *naux* < 300|An input-argument error message is issued. The value in the error message is the minimum required value, 300. The application program stops.|ESSL returns the value of *naux* as 300 to the application program, and an input-argument error message is issued. The value in the error message is the minimum required value, 300. ESSL does no computation, and control is returned to the application program.|
|*naux* \geq 300|Your application program runs successfully.|Your application program runs successfully.|

# Here Is How You Code It in Your Program

If you leave error 2015 unrecoverable, you **do not code anything** in your program. You just look at the error messages to get the sizes of auxiliary storage. On the other hand, if you want to make error 2015 recoverable to obtain the auxiliary storage sizes dynamically in your program, you need to **add some coding statements** to your program. For details on coding these statements in each programming language, see the following examples:

+   - For Fortran, see page 116
+   - For C, see page 134
+   - For C++, see page 150

You may want to provide a separate subroutine to calculate the auxiliary storage size whenever you need it. Figure 3 on page 38 shows how you might code a separate Fortran subroutine. Before calling SCFT in your program, call this subroutine, SCFT which calculates the minimum size and stores it in the \textit{nux} arguments. Upon return, your program checks the return code. If it is nonzero, the \textit{nux} arguments were updated, as planned. You should then make sure adequate storage is available and call SCFT. On the other hand, if the return code is zero, error handling was not invoked, the \textit{nux} arguments were not updated, and the initialization step was performed for SCFT.