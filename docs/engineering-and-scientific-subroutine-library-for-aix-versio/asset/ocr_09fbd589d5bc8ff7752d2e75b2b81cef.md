Errors in C” on page 131 and in step 1 in “Computational Errors in C” on page 136. The two types of ESSL arguments are:
• *naux* arguments for auxiliary storage
• *n* arguments for transform lengths

# ## Setting Up a User-Supplied Subroutine for ESSL in C

Some ESSL numerical quadrature subroutines call a user-supplied subroutine, *subf*, identified in the ESSL calling sequence. If your program that calls the numerical quadrature subroutines is coded in C, there are some coding rules you must follow for the *subf* subroutine:
• You can code the *subf* subroutine using only C or Fortran.
• You must declare *subf* as an external subroutine in your application program.
• You should code the *subf* subroutine to the specifications given in “Programming Considerations for the SUBF Subroutine” on page 914. For an example of coding a *subf* subroutine in C, see “Example 1” on page 924.

# ## Setting Up Scalar Data in C

Table 31 lists the scalar data types in C that are used for ESSL. Only those types and lengths used by ESSL are listed.

![](bbox=[0.26, 0.4, 0.88, 0.82])