
## SURXOR and DURXOR

*vseed* is the work area used by these subroutines, containing the new seed that is to be used in subsequent calls to this subroutine. Returned as: a one-dimensional array of (at least) length 10000, containing numbers of the data type indicated in Table 177 on page 947.

### Notes

1. You can generate the same vector x of random numbers by starting over and specifying your original nonzero *iseed* value.
2. Multiple calls to these subroutines with mixed sizes generate the same sequence of numbers as a single call the total length, assuming you specify the same initial *iseed* in both cases. For example, you can generate the same vector x of random numbers by calling this subroutine twice and specifying n = 10 or by calling this subroutine once and specifying n = 20. You need to specify the same *iseed* in the initial call in both cases, and *iseed* = 0 in the second call with n = 10.
3. Vector x must have no common elements with the storage area specified for *vseed*; otherwise, results are unpredictable.
4. In your C program, argument *iseed* must be passed by reference.

### Function

The pseudo-random numbers uniformly distributed in the interval [0,1) are generated using the Taustworthe exclusive-or algorithm. This is based on a linear-feedback shift-register sequence. The very long period of the generator, $2^{129} - 1$, makes it useful in modern statistical simulations where the shorter period of other generators could be exhausted during a single run. If you need a large number of random numbers, you can use these subroutines, because with this generator you do not request more than a small percentage of the entire period of the generator.

This generator is based on two feedback positions to generate a new binary digit:

$$
\begin{aligned}
\mathbf{z}_k & = \mathbf{z}_{(k-p)} \oplus \mathbf{z}_{(k-q)} \\
\text{where:} \\
& p > q \\
& k = 1, 2, \dots \\
& \mathbf{z} \text{ is a bit vector.} \\
& \text{and where:} \\
& \oplus \text{ is the bitwise exclusive-or operation.}
\end{aligned}
$$

For details, see references [55], [76], and [97]. The values of p and q are selected according to the criteria stated in reference [103].

The algorithm initializes a seed vector of length p, starting with *iseed*. The seed vector is stored in *vseed* for use in subsequent calls to this subroutine with *iseed* = 0.

If n is 0, no computation is performed, and the initial seed is unchanged.

### Special Usage

For some specialized applications, if you need multiple sources of random numbers, you can specify different *vseed* areas, which are initialized with different seeds on multiple calls to this subroutine. You then get multiple sequences of the random number sequence provided by the generator that are sufficiently far apart for most purposes.

### Error Conditions

Computational Errors: None.

Input-Argument Errors:

1. n < 0
2. vseed = 0 and vseed does not contain valid data.

### Example 1

This example shows a call to SURXOR to generate 10 random numbers.

Call Statement and Input:

```
ISeed
N
X
VSEED
| | | |
CALL SURXOR( ISeed , 10 , X , VSEED )

ISeed = 137
```

Output:

```
ISeed = 0
X = (0.6440868,
0.5105118,
0.4878680,
0.3209075,
0.6624528,
0.2499877,
0.0056630,
0.7329214,
0.7486335,
0.8050517)
```

### Example 2

This example shows a call to SURXOR to generate 10 random numbers. This example specifies vseed = 0 and uses the vseed output generated from Example 1.

Call Statement and Input:

```
ISeed
N
X
VSEED
| | | |
CALL SURXOR( ISeed , 10 , X , VSEED )

ISeed = 0
```

Output:

```
ISeed = 0
X = (0.9930249,
0.0441873,
0.6891295,
0.3101060,
0.6324178,
0.3299408,
0.3553145,
0.0100013,
0.0214620,
0.8059390)
```

### Example 3

This example shows a call to DURXOR to generate 20 random numbers. This sequence of numbers generated are like those generated in Examples 1 and 2.

Call Statement and Input:

```
ISEED       N    X    VSEED
  |         |    |    |
CALL DURXOR( ISEED , 20 , X , VSEED )

ISEED       = 137
```

Output:

```
ISEED       = 0

X           = (0.64408693438956721,
              0.51051182536460882,
              0.48786801310787142,
              0.32090755617007050,
              0.66245283144861666,
              0.24998782843358081,
              0.00566308101257373,
              0.73292147005172925,
              0.74863359794102236,
              0.80505169697755319,
              0.99302499462139138,
              0.04418740640269125,
              0.68912952155409579,
              0.31010611495627916,
              0.63241786342211936,
              0.32994081459690583,
              0.35531452631408911,
              0.01001344131325811,
              0.02146199494672940,
              0.80593898487597615)
```

## Chapter 17. Utilities

The utility subroutines are described in this chapter.

### Overview of the Utility Subroutines

The utility subroutines perform general service functions that support ESSL, rather than mathematical computations (Table 178).

**Table 178. List of Utility Subroutines**

| Descriptive Name | Subroutine | Page |
|---|---|---|
| ESSL Error Information-Handler Subroutine | EINFO | 954 |
| ESSL ERRSAV Subroutine for ESSL | ERSAV | 957 |
| ESSL ERRSET Subroutine for ESSL | ERRSET | 958 |
| ESSL ERRSTR Subroutine for ESSL | ERRSTR | 960 |
| Set the Vector Section Size (VSS) for the ESSL/370 Scalar Library | IVSSET† | |
| Set the Extended Vector Operations Indicator for the ESSL/370 Scalar Library | IEOPS† | |
| Determine the Level of ESSL Installed | IESSL | 961 |
| Determine the Stride Value for Optimal Performance in Specified Fourier Transform Subroutines | STRIDE | 963 |
| Convert a Sparse Matrix from Storage-by-Rows to Compressed-Matrix Storage Mode | DRSRM | 972 |
| For a General Sparse Matrix, Convert Between Diagonal-Out and Profile-In Skyline Storage Mode | DGKTRN | 976 |
| For a Symmetric Sparse Matrix, Convert Between Diagonal-Out and Profile-In Skyline Storage Mode | DSKTRN | 981 |

† This subroutine is provided for migration from earlier releases of ESSL and is not intended for use in new programs. Documentation for this subroutine is no longer provided.

### Use Considerations

This section describes what you use the utility subroutines for.

#### Determining the Level of ESSL Installed

IESSL gets the level of ESSL and returns it to your program. The level consists of the following: version number, release number, modification number, and number of the most recently installed ESSL PTF. You can use this function to verify that you are running on or using the capabilities of the desired level.

#### Finding the Optimal Stride(s) for Your Fourier Transforms

STRIDE is used to determine optimal stride values for your Fourier transforms when using any of the Fourier transform subroutines, except _RCFT and _CRFT. You must invoke STRIDE for each optimal stride you want computed. Sometimes you need a separate stride for your input and output data. For the three-dimensional Fourier transforms, you need an optimal stride for both the second and third dimensions of the array. The examples provided for STRIDE explain how it is used for each of the subroutines listed above.

After obtaining the optimal strides from STRIDE, you should arrange your data using these stride values. After the data is set up, call the Fourier transform subroutine. For additional information on how to set up your data, see “Setting Up Your Data” on page 746.

#### Converting Sparse Matrix Storage

DSRSM is used to migrate your existing program from sparse matrices stored by rows to sparse matrices stored in compressed-matrix storage mode. This converts the matrices into a storage format that is compatible with the input requirements for some ESSL sparse matrix subroutines, such as DSMX.

DGKTRN and DSKTRN are used to convert your sparse matrix from one skyline storage mode to another, if necessary, before calling the subroutines DGKFS/DGKFSP or DSKFS/DSKFSP, respectively.
