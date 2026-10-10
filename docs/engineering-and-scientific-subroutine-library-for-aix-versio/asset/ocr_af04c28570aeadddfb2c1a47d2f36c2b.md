# ## Setting Up Scalar Data in Fortran

Table 30 lists the scalar data types in Fortran that are used for ESSL. Only those types and lengths used by ESSL are listed.

# *Table 30. Scalar Data Types in Fortran Programs*

| Terminology Used by ESSL | Fortran Equivalent |
| :--- | :--- |
| Character item¹ | CHARACTER*1 |
| 'N', 'T', 'C' or 'n', 't', 'c' | 'N', 'T', 'C' |
| Logical item | LOGICAL |
| .TRUE., .FALSE. | .TRUE., .FALSE. |
| 32-bit environment integer | INTEGER or INTEGER*4 |
| 12345, -12345 | 12345, -12345 |
| 64-bit environment integer² | INTEGER*8³ |
| 12345, -12345 | 12345_8, -12345_8 |
| Short-precision real number⁴ | REAL or REAL*4 |
| 12.345 | 0.12345E2 |
| Long-precision real number⁴ | DOUBLE PRECISION or REAL*8 |
| 12.345 | 0.12345D2 |
| Short-precision complex number⁴ | COMPLEX or COMPLEX*8 |
| (123.45, -54321.0) | (123.45E0, -543.21E2) |
| Long-precision complex number⁴ | COMPLEX*16 |
| (123.45, -54321.0) | (123.45D0, -543.21D2) |

Note: ¹ ESSL accepts character data in either upper- or lowercase in its calling sequences.

² In accordance with the LP64 data model, all ESSL integer arguments remain 32-bits except for the *iusadr* argument for ERRSET.

³ INTEGER may be used if you specify the compiler option *-qintsize=8*.

⁴ Short- and long-precision numbers look the same in this book.

# ## Setting Up Arrays in Fortran

Arrays are declared in Fortran by specifying the array name, the number of dimensions, and the range of each dimension in a DIMENSION statement or an explicit data type statement, such as REAL, DOUBLE PRECISION, and so forth.

# ### Real and Complex Array Elements

Each array element can be either a real or complex data item of short or long precision. The type of the array determines the size of the element storage locations. Short-precision data requires 4 bytes, and long-precision data requires 8 bytes. Complex data requires two storage locations of either 4 or 8 bytes each, for short or long precision, respectively, to accommodate the two parts of the complex number: c = a+bi. Therefore, exactly twice as much storage is required for complex data as for real data of the same precision. See “How Do You Set Up Your Scalar Data?” on page 29 for a description of real and complex numbers.