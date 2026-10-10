| ESLS Library Name | Command |
| :--- | :--- |
| | `cc -O xyz.c -lessl` |
| Serial | | `cc -O -D_CMLPX -D_DCMPLX xyz.c -lessl` |
| | | `cc -O -q64 xyz.c -lessl` |
| 32-bit | | |
| | | `cc -O -D_CMLPX -D_DCMPLX -q64 xyz.c -lessl` |
| 64-bit | | |

# ## C++ Program Procedures

The ESL header file *ess1.h*, used for C and C++ programs, is installed in the *~usr/include* directory. When using ESL, the compiler option **-qnocinc=/usr/include/essl** must be specified.

If you are using the IBM Open Class Complex Mathematics Library, you automatically use the definition of short-precision complex data provided in the ESL header file. If you prefer to specify your own definition for short-precision complex data, add **-D_CMLPX** to your commands (as shown in the table below). Otherwise, ESL will use the IBM Open Class Complex Mathematics Library or the Standard Numerics Library, as described in “On AIX—Selecting the `<complex>` or `<complex.h>` Header File” on page 143.

If you prefer to explicitly specify that you want to use the Standard Numerics Library facilities for complex arithmetic, add **-D_ESV_COMPLEX_** to your command as shown in the table below.

The ESL header file supports two alternatives for declaring scalar output arguments. By default, the arguments are declared to be type reference. If you prefer for them to be declared as pointers, add **-D_ESVCPTP** to your commands as shown in the table below.

When linking and running your program, you must modify your existing job procedures for ESL, to set up the necessary libraries.

If you are accessing ESL from a C++ program, you can compile and link using the commands shown in the table below.

| ESLS Library Name | Command |
| :--- | :--- |
| | `xlC_r -O xyz.c -lesslsmp -qnocinc=/usr/include/essl` |
| | | `xlC_r -O -D_CMLPX xyz.c -lesslsmp -qnocinc=/usr/include/essl` |
| | | `xlC_r -O -D_ESV_COMPLEX_ xyz.c -lesslsmp -qnocinc=/usr/include/essl` |
| | | `xlC_r -O -D_ESVCPTP xyz.c -lesslsmp -qnocinc=/usr/include/essl` |
| | | |
| SMP | 32-bit | `xlC_r -O -q64 xyz.c -lesslsmp -qnocinc=/usr/include/essl` |
| | | `xlC_r -O -D_CMLPX -q64 xyz.c -lesslsmp -qnocinc=/usr/include/essl` |
| | | `xlC_r -O -D_ESV_COMPLEX_ -q64 xyz.c -lesslsmp -qnocinc=/usr/include/essl` |
| | 64-bit | `xlC_r -O -D_ESVCPTP -q64 xyz.c -lesslsmp -qnocinc=/usr/include/essl` |